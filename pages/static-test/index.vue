<template>
  <div>
    <h1>Static Test Page</h1>
    <p>This page should be prerendered as static HTML.</p>
    <p>If you can see this after refreshing the page at /static-test, then the issue is resolved.</p>
    <p>If you get a 502 error when refreshing at /static-test, then the issue is reproduced.</p>
    <NuxtLink to="/">Back to Home</NuxtLink>
  </div>
</template>
