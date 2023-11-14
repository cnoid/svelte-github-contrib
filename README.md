# svelte-github-contrib
Display GitHub contributions in Sveltekit

![image](https://github.com/cnoid/svelte-github-contrib/assets/10182309/0ec03dd6-6520-490e-8a10-acd85aac2549)


Runs using [GitHub Contributions API](https://github.com/mattcroat/github-contributions-api) - Dockerfile is in this repo if you want to run it containerized, just place it in the folder after cloning and run docker build.


Usage:


```js
<script>
  <!-- The rest of your imports and such -->
  import { onMount } from 'svelte';
  import GitHubTable from '$lib/GitHubTable.svelte';

  let contributions = [];

  onMount(async () => {
    try {
      const response = await fetch('https://yourapi.com/user/year');
      if (response.ok) {
        contributions = await response.json();
      } else {
        console.error('Error fetching contributions:', response.status);
      }
    } catch (error) {
      console.error('Network error:', error);
    }
  });
</script>
```

No error handling:

```js
<script>
  <!-- The rest of your imports and such -->
  import { onMount } from 'svelte';
  import GitHubTable from '$lib/GitHubTable.svelte';

  let contributions = [];

  onMount(async () => {
    const response = await fetch('https://yourapi.com/user/year');
    if (response.ok) {
      contributions = await response.json();
    }
  });
</script>
```

Simply insert where you want it:
`<GitHubTable {contributions} />`

Note that the CSS is for dark mode and is not complete depending on your usage. CSS is simply not my forte.
