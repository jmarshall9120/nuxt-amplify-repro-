# Nuxt Amplify Hosting Issue Reproduction

This project reproduces the issue described in [amplify-js#14606](https://github.com/aws-amplify/amplify-js/issues/14606) where Nuxt prerendered pages fail to load on refresh when hosted on AWS Amplify.

## Issue Description

When a Nuxt app is deployed to Amplify Hosting with prerendered routes:
- Accessing `/static-test/index.html` works correctly (200 OK)
- Accessing `/static-test` fails with 502 Bad Gateway on refresh
- The server tries to find the file at `/static/test-static/index.html` but it's not there

## Setup

1. Install dependencies:
```bash
npm install
```

2. Build the project:
```bash
npm run build
```

## Reproduction Steps

1. Deploy this app to AWS Amplify Hosting
2. Navigate to the deployed URL
3. Click "Go to Static Test Page" to navigate to `/static-test`
4. Refresh the page while on `/static-test`
5. Observe the 502 Bad Gateway error

## Expected Behavior

The `/static-test` route should serve the prerendered HTML content without errors, just like `/static-test/index.html` does.

## Configuration

The key configuration in `nuxt.config.ts`:

```typescript
nitro: {
  preset: 'aws-amplify',
  awsAmplify: {
    catchAllStaticFallback: true
  },
  routeRules: {
    '/static-test': { prerender: true }
  }
}
```

This configuration should prerender the `/static-test` route as static HTML, but the routing fails when accessed without the explicit `/index.html` suffix.
