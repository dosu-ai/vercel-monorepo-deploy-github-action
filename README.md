# Vercel Preview Deployment Workflow

This workflow automates the deployment of preview environments for pull requests using Vercel. It supports multiple projects and dynamically updates deployment URLs in a pull request comment.

## How to Use

### Copying the File
To use this workflow in your repository:
1. Copy this file into `.github/workflows/vercel-preview.yml` in your repository.
2. Ensure you have the necessary secrets and permissions configured.

### Required Secrets
Set the following secrets in your repository:
- **`VERCEL_TOKEN`**: Your Vercel API token.
- **`VERCEL_ORG_ID`**: Your Vercel organization ID.
- **`VERCEL_[PROJECT_NAME]_PROJECT_ID`**: Project ID for your Vercel project(s).

Replace `[PROJECT_NAME]` and `[PROJECT_NAME_2]` with the actual names of your projects.

### Customizing the Workflow
1. **Organization and Project Details**  
   Update the following placeholders:
   - `[PROJECT_NAME]` and `[PROJECT_NAME_2]` with your project names.
   - `[path_to_project]` and `[path_to_project_2]` with the relative paths to your projects.
   - `[org_name]` with your Vercel organization name.

2. **Matrix Configuration**  
   Add or remove projects in the `strategy.matrix.include` section to deploy additional projects.

3. **Environment Variables**  
   Ensure each project-specific variable, like `VERCEL_[PROJECT_NAME]_PROJECT_ID`, matches your configuration.

### Features
- **Deployment Artifacts**: Each project is built and deployed separately.
- **PR Comment Updates**: The workflow comments on the pull request with deployment URLs, updating them as deployments complete.
- **Concurrent Deployment Handling**: Uses `concurrency` to manage simultaneous runs and prevent overlapping deployments.

### Notes
- The workflow uses `actions/cache` for faster builds by caching the `pnpm` store.
- Deployment data is managed using artifacts to track existing deployments.
- `jq` is used for JSON manipulation. Ensure your environment supports it.

### Example Comment Output
After running the workflow, the pull request will include a comment like this:

