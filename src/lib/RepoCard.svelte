<script>
  export let repo;
</script>

<div class="repo-card">
  <a href={repo.html_url} target="_blank" rel="noopener noreferrer" class="repo-name">
    {repo.name}
  </a>
  <div class="repo-description">
    {repo.description || 'No description available'}
  </div>
  
  {#if repo.homepage}
    <div class="repo-links">
      <a href={repo.homepage} target="_blank" rel="noopener noreferrer" class="website-link">
        <svg class="icon" viewBox="0 0 16 16" fill="currentColor">
          <path d="M8 0a8 8 0 1 1 0 16A8 8 0 0 1 8 0ZM5.78 8.75a9.64 9.64 0 0 0 0 1.5c.263.837.752 1.57 1.46 2.188A7.015 7.015 0 0 0 5.78 8.75Zm.979-1.75a8.993 8.993 0 0 0 0 2h2.482a8.993 8.993 0 0 0 0-2H6.76ZM8 12.5c-.534 0-1.044-.276-1.534-.82-.49-.543-.867-1.263-1.131-2.055a8.993 8.993 0 0 1 0-3.25c.264-.792.64-1.512 1.13-2.055C7.957 3.776 8.466 3.5 8 3.5c.534 0 1.044.276 1.534.82.49.543.867 1.263 1.131 2.055a8.993 8.993 0 0 1 0 3.25c-.264.792-.64 1.512-1.13 2.055-.491.544-1 .82-1.535.82Zm1.76-4.75c.001.667.068 1.334.2 2h2.482a8.993 8.993 0 0 0 0-2H9.76Zm2.54 2.75a9.64 9.64 0 0 0 0-1.5 7.015 7.015 0 0 0 1.46-4.188A7.015 7.015 0 0 0 12.3 8.75a9.64 9.64 0 0 0 0 1.5Z"/>
        </svg>
        🌐 Website
      </a>
    </div>
  {/if}
  
  <div class="repo-meta">
    {#if repo.language}
      <span class="language">{repo.language}</span>
    {/if}
    <div class="meta-item">
      <svg class="icon" viewBox="0 0 16 16" fill="currentColor">
        <path d="M8 .25a.75.75 0 01.673.418l1.882 3.815 4.21.612a.75.75 0 01.416 1.279l-3.046 2.97.719 4.192a.75.75 0 01-1.088.791L8 12.347l-3.766 1.98a.75.75 0 01-1.088-.79l.72-4.194L.818 6.374a.75.75 0 01.416-1.28l4.21-.611L7.327.668A.75.75 0 018 .25z"/>
      </svg>
      {repo.stargazers_count}
    </div>
    <div class="meta-item">
      <svg class="icon" viewBox="0 0 16 16" fill="currentColor">
        <path d="M5 3.25a.75.75 0 11-1.5 0 .75.75 0 011.5 0zm0 2.122a2.25 2.25 0 10-1.5 0v.878A2.25 2.25 0 005.75 8.5h1.5v2.128a2.251 2.251 0 101.5 0V8.5h1.5a2.25 2.25 0 002.25-2.25v-.878a2.25 2.25 0 10-1.5 0v.878a.75.75 0 01-.75.75h-4.5A.75.75 0 015 6.25v-.878zm3.75 7.378a.75.75 0 11-1.5 0 .75.75 0 011.5 0zm3-8.75a.75.75 0 100-1.5.75.75 0 000 1.5z"/>
      </svg>
      {repo.forks_count}
    </div>
  </div>
</div>
