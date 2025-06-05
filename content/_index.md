+++
title = 'Too Short to Not Read'
layout = 'single'
description = 'Simple and fast guide-style website, no ads, no bloat, no fluff.'
+++
## What do you want to do?

<div class="search js-only">
  <input id="search" type="text" placeholder="Search guides..." />
  <button id="clear-search" title="Clear search">✖</button>
</div>


<script>

document.addEventListener("DOMContentLoaded", () => {
  for (const e of document.getElementsByClassName("js-only")) {
    e.classList.remove("js-only");
  }

  const guides = document.querySelectorAll("#artlist li");
  const search = document.getElementById("search");
  const clearSearch = document.getElementById("clear-search");
  const artlist = document.getElementById("artlist");

  search.addEventListener("input", () => {
    const searchText = search.value.toLowerCase().trim().normalize('NFD').replace(/\p{Diacritic}/gu, "");
    const searchTerms = searchText.split(" ");
    const hasFilter = searchText.length > 0;

    artlist.classList.toggle("list-searched", hasFilter);

    guides.forEach(guide => {
      const searchString = `${guide.textContent} ${guide.dataset.tags}`.toLowerCase().normalize('NFD').replace(/\p{Diacritic}/gu, "");
      const isMatch = searchTerms.every(term => searchString.includes(term));

      guide.hidden = !isMatch;
      guide.classList.toggle("matched-recipe", hasFilter && isMatch);
    });
  });

  clearSearch.addEventListener("click", () => {
    search.value = "";
    guides.forEach(guide => {
      guide.hidden = false;
      guide.classList.remove("matched-recipe");
    });
    artlist.classList.remove("list-searched");
  });
});

</script>

## Check out these new guides!

{{< artlist >}}

## Or Browse by Category...

{{< tagcloud >}}

## Learn about this website
Read the [about](/about/about) page to learn more about this website.
