<script>
  export let repos;

  $: totalStars = repos.reduce((sum, repo) => sum + repo.stargazers_count, 0);
  $: totalForks = repos.reduce((sum, repo) => sum + repo.forks_count, 0);
</script>

<div class="stats">
  <div class="stat">
    <div class="stat-value">{repos.length}</div>
    <div class="stat-label">Public Repositories</div>
  </div>
  <div class="stat">
    <div class="stat-value">{totalStars}</div>
    <div class="stat-label">Total Stars</div>
  </div>
  <div class="stat">
    <div class="stat-value">{totalForks}</div>
    <div class="stat-label">Total Forks</div>
  </div>
</div>
