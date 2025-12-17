The imagined application is an API built with Python (FastAPI) connected to a Supabase database. The app is deployed on Google Cloud Run. The purpose is to allow users (other apps) to access the sophisticated prompt pipeline that the team has developed. Endpoints are things like "/solve-disagreement", where the user sends information about a disagreement between two or more parties, and the API returns an elegant solution to the disagreement.

Linting: The team is encouraged to use ruff in their IDE. They also have a pre-commit hook that runs ruff. This ensures that poorly formatted code is never committed.

Testing: Tests are written using Pytest, and make use of `fastapi.testclient`, the built-in test client in FastAPI. The team has a GitHub Action that runs tests on every push on any branch for files that changed.

Building: GitHub action that sets up python, installs dependencies with pip, runs tests, builds a docker image (and pushes to registry and deploys, if main branch.) Python is interpreted, so we don't need to 'create a build'.

Alternatives for Jenkins/GH Actions: Google Cloud Build could be good, it can trigger from Git repos. AWS and Azure have their own options too (AWS CodePipeline, Azure Pipelines) but they don't make sense since we're deployed on GCP. GitLab and Bitbucket also have their own solutions, but we're using GitHub. Standalone: CircleCI, TravisCI, ...

Cloud-based, because it's a simple use case and a small team with no special hardware needs. Likely simpler and cheaper at this scale. On the other hand, if the API was handling very sensitive information, or we were running our own AI models, we could reconsider and move both the deployment and CI to a self-hosted server.
