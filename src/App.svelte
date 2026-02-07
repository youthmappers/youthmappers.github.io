<script>
  import { onMount } from 'svelte';
  import RepoCard from './lib/RepoCard.svelte';
  import Stats from './lib/Stats.svelte';

  const GITHUB_ORG = 'youthmappers';
  const API_URL = `https://api.github.com/orgs/${GITHUB_ORG}/repos`;
  const EXCLUDED_REPOS = ['.github', 'youthmappers.github.io'];

  let repos = [];
  let loading = true;
  let error = '';

  async function fetchAllRepositories() {
    const allRepos = [];
    let page = 1;
    const perPage = 100;

    try {
      while (true) {
        const response = await fetch(`${API_URL}?type=public&sort=updated&per_page=${perPage}&page=${page}`);
        
        // Check rate limits
        const rateLimit = response.headers.get('X-RateLimit-Remaining');
        const rateLimitReset = response.headers.get('X-RateLimit-Reset');
        
        if (rateLimit !== null && parseInt(rateLimit) < 5) {
          const resetTime = new Date(parseInt(rateLimitReset) * 1000);
          console.warn(`Approaching rate limit. Resets at ${resetTime.toLocaleTimeString()}`);
        }
        
        if (!response.ok) {
          if (response.status === 403 && rateLimit === '0') {
            throw new Error('GitHub API rate limit exceeded. Please try again later.');
          }
          throw new Error(`GitHub API returned ${response.status}: ${response.statusText}`);
        }

        const reposBatch = await response.json();
        
        if (reposBatch.length === 0) {
          break; // No more repositories
        }
        
        allRepos.push(...reposBatch);
        
        // If we got fewer than perPage results, we've reached the end
        if (reposBatch.length < perPage) {
          break;
        }
        
        page++;
      }
      
      return allRepos;
    } catch (err) {
      throw err;
    }
  }

  async function loadRepositories() {
    try {
      loading = true;
      error = '';
      
      const allRepos = await fetchAllRepositories();
      
      // Filter out archived repositories and excluded repos, then sort by stars
      repos = allRepos
        .filter(repo => !repo.archived && !EXCLUDED_REPOS.includes(repo.name))
        .sort((a, b) => b.stargazers_count - a.stargazers_count);
      
      loading = false;
    } catch (err) {
      console.error('Error fetching repositories:', err);
      error = `Failed to load repositories: ${err.message}`;
      loading = false;
    }
  }

  onMount(() => {
    loadRepositories();
  });
</script>

<div class="container">
  <header>
    <h1>🗺️ YouthMappers Labs</h1>
    <p>Showcasing innovative projects from YouthMappers chapters worldwide</p>
  </header>

  <div class="content">
    {#if !loading && repos.length > 0}
      <Stats {repos} />
    {/if}

    {#if loading}
      <div class="loading">Loading repositories...</div>
    {/if}

    {#if error}
      <div class="error">{error}</div>
    {/if}

    {#if !loading && !error && repos.length === 0}
      <p>No public repositories found.</p>
    {/if}

    {#if !loading && repos.length > 0}
      <div class="repositories">
        {#each repos as repo (repo.id)}
          <RepoCard {repo} />
        {/each}
      </div>
    {/if}
  </div>

  <footer>
    <p>
      Made with ❤️ by <a href="https://www.youthmappers.org" target="_blank">YouthMappers</a> | 
      <a href="https://github.com/youthmappers" target="_blank">View on GitHub</a>
    </p>
  </footer>
</div>
