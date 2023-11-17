# svelte-github-contrib
Display GitHub contributions in Sveltekit

<details>
  <summary>Matia's scraper</summary>

![image](https://github.com/cnoid/svelte-github-contrib/blob/4abe1c1c3c0c5991707d8d5e19004466d517a3fe/Screenshot%202023-11-14%20144156.png)

</details>


![image](https://github.com/cnoid/svelte-github-contrib/blob/6f6358db6157362efb4561744e1ce5a9b988b23b/contrib-api.png)

Runs using [GitHub Contributions API](https://github.com/mattcroat/github-contributions-api) - Dockerfile is in this repo if you want to run it containerized, just place it in the folder after cloning and run docker build.


Usage:

Step 1: Pick your poison

Step 2: Download the version that goes with what you decided on.

Some notes about it: contrib-api uses GraphQL (which means getting a token), while Matia's version uses scraping with SvelteKit. It's only a matter of preference as both return JSON. The scraper returns all days of the year, however, while the GraphQL updates in the same way Github profile does. (currentdate - 370 days)

The scraper is easiest because you can simply use the one [he is hosting on Vercel](https://gh-contributions-api.vercel.app/), while the other is more reliable as it's using Github's GraphQL.


### [contrib-api](https://github.com/cnoid/contrib-api)

<details>
  <summary>Expand</summary>

  
  ```js
  <!-- The rest of your header/imports -->
  import GitHubTable from '$lib/GitHubTable.svelte';
  import { onMount } from 'svelte';

  let contributions = [];

  onMount(async () => {
    try {
      const response = await fetch('https://example.com/api/contrib?userName=yourusername');
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

Or, no error logging:

  ```js
  <!-- The rest of your header/imports -->
  import GitHubTable from '$lib/GitHubTable.svelte';
  import { onMount } from 'svelte';

  let contributions = [];

  onMount(async () => {
    try {
      const response = await fetch('https://example.com/api/contrib?userName=yourusername');
      if (response.ok) {
        contributions = await response.json();
      } 
  });
</script>
```
</details>


### [Matia's SvelteKit scraper](https://github.com/mattcroat/github-contributions-api)

<details>
  <summary>Expand</summary>
Insert into your header:
  
```js
<script>
  <!-- The rest of your imports and such -->
  import { onMount } from 'svelte';
  import GitHubTable from '$lib/GitHubTable.svelte';

  let contributions = [];

  onMount(async () => {
    try {
      const response = await fetch('https://example.com/user/year');
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
    const response = await fetch('https://example.com/user/year');
    if (response.ok) {
      contributions = await response.json();
    }
  });
</script>
```
</details>

Step 3:

Simply insert where you want it:
`<GitHubTable {contributions} />`

Note that the CSS is for dark mode and is not complete depending on your usage. CSS is simply not my forte.
