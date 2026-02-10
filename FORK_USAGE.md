# What You Can Do With This Fork

This document explains the various ways you can use and customize this fork of the free-llm-api-resources repository.

## Overview

This repository automatically tracks and maintains a comprehensive, up-to-date list of free LLM (Large Language Model) API resources from various providers. The README is automatically generated through a Python script that fetches the latest model availability and rate limits from multiple providers.

## Use Cases

### 1. **Keep Your Own List of Free LLM Resources**

This fork allows you to maintain your own curated list of free LLM API providers. You can:

- Track providers you personally use or trust
- Remove providers you don't need
- Add custom notes or modifications for your specific use cases
- Maintain your own versioning history

### 2. **Customize the List for Your Needs**

You can modify the list to:

- **Filter by specific model types**: Focus on only text models, vision models, or speech models
- **Add private API keys**: The automation script supports adding your API keys in `.env` file
- **Customize rate limit tracking**: Modify `src/pull_available_models.py` to track different metrics
- **Add your own providers**: Include local or internal services in your organization

### 3. **Automate Model Availability Tracking**

The repository includes GitHub Actions workflows that:

- **Run daily updates**: Automatically check for new models and updated rate limits
- **Generate pull requests**: Create PRs with changes for review before merging
- **Validate changes**: Ensure README modifications don't break the structure

To enable automatic updates in your fork:

1. Add the required API keys as GitHub Secrets in your repository settings:
   - `GROQ_API_KEY`
   - `CLOUDFLARE_ACCOUNT_ID`
   - `CLOUDFLARE_API_KEY`
   - `HYPERBOLIC_API_KEY`
   - `GCP_PROJECT_ID`
   - `LAMBDA_API_KEY`
   - `MISTRAL_API_KEY`
   - `SCALEWAY_API_KEY`
   - `COHERE_API_KEY`
   - Google Cloud authentication credentials

2. The workflow runs daily at midnight UTC, or you can trigger it manually from the Actions tab

### 4. **Run Local Updates**

You can run the update script locally for testing or one-off updates:

```bash
# Install dependencies
pip install -r src/requirements.txt

# Set up your API keys in a .env file
# Then run the script
python src/pull_available_models.py
```

This will fetch the latest models and update the README.md file.

### 5. **Contribute New Providers**

You can add support for new LLM API providers by:

1. **Adding provider-specific logic** to `src/pull_available_models.py`
2. **Updating the model name mapping** in `src/data.py`
3. **Modifying the template** in `src/README_template.md` if needed

Example structure for adding a new provider:

```python
def fetch_new_provider_models():
    # Fetch models from the provider API
    # Return formatted model list with rate limits
    pass
```

### 6. **Create a Custom Version for Your Organization**

If you're part of an organization, you can:

- Add internal LLM services to the list
- Include organization-specific rate limits or quotas
- Customize the documentation format for internal wikis
- Track which models are approved for use within your company

### 7. **Learn How to Build API Aggregation Tools**

This repository serves as a great example of:

- API rate limit detection and tracking
- Automated documentation generation
- GitHub Actions workflows for data updates
- Python API clients and web scraping techniques

### 8. **Monitor Provider Changes Over Time**

By keeping your fork updated:

- Track when providers add or remove models
- Monitor rate limit changes over time
- Get notified when new free tiers become available
- Archive historical data through git history

## Repository Structure

```
.
├── README.md                          # Auto-generated list (DO NOT EDIT MANUALLY)
├── src/
│   ├── pull_available_models.py      # Main script that fetches model data
│   ├── data.py                       # Model name mappings and ignored models
│   ├── README_template.md            # Template for README generation
│   └── requirements.txt              # Python dependencies
├── .github/
│   └── workflows/
│       ├── update-readme.yml         # Daily update workflow
│       └── readme-change-validator.yml # Validation workflow
└── FORK_USAGE.md                     # This file
```

## Customization Guide

### Modify Model Name Mappings

Edit `src/data.py` to customize how model IDs are displayed:

```python
MODEL_TO_NAME_MAPPING = {
    "model-id": "Human Readable Name",
    # Add your custom mappings here
}
```

### Ignore Specific Models

Add models to ignore lists in `src/data.py`:

```python
OPENROUTER_IGNORED_MODELS = {
    "model-to-ignore:free",
}
```

### Change the README Format

Modify `src/README_template.md` to change how the README is structured:

- Change headings
- Add custom sections
- Modify table formats
- Add warnings or notes

### Add Custom Provider Sections

You can add static sections to the README template that won't be overwritten by the automatic updates, such as:

- Usage examples
- Authentication guides
- Best practices
- Your own notes

## Best Practices

1. **Don't manually edit README.md** - It's auto-generated. Make changes to the template or script instead.
2. **Keep your fork synced** - Regularly pull updates from the upstream repository to get new providers and improvements.
3. **Use branches** - Create feature branches when adding new providers or making significant changes.
4. **Test locally first** - Run the script locally before pushing changes to GitHub Actions.
5. **Secure your API keys** - Never commit API keys to the repository. Use GitHub Secrets or `.env` files (which are gitignored).

## Contributing Back to Upstream

If you add features or new providers that could benefit everyone:

1. Test your changes thoroughly in your fork
2. Create a pull request to the upstream repository
3. Follow the guidelines in `.github/pull_request_template.md`
4. Ensure providers meet the legitimacy criteria

## Common Customizations

### Add a "Favorites" Section

Create a custom section in the template for your most-used providers:

```markdown
## My Favorite Providers

- **OpenRouter**: Great variety of models
- **Groq**: Extremely fast inference
- **Cerebras**: High token limits
```

### Track Additional Metadata

Modify the script to track custom information:

- Response time/latency
- Model quality ratings
- Context window sizes
- Supported features (function calling, streaming, etc.)

### Create a Simplified View

Generate a second markdown file with just the essentials:

- Only your top 5 providers
- Quick reference table
- Direct API endpoint URLs

## Troubleshooting

### Workflow Fails

- Check that all required API keys are set in GitHub Secrets
- Review the Actions logs for specific error messages
- Ensure you have write permissions to the repository

### Script Errors Locally

- Verify all dependencies are installed: `pip install -r src/requirements.txt`
- Check that your `.env` file contains valid API keys
- Ensure you have internet connectivity for API calls

### README Not Updating

- Check if the workflow is enabled in the Actions tab
- Verify the cron schedule in `.github/workflows/update-readme.yml`
- Manually trigger the workflow to test it

## Further Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Python Requests Library](https://requests.readthedocs.io/)
- [Working with Forks](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks)

## Questions or Ideas?

Feel free to:
- Open an issue in your fork to track your own customization ideas
- Experiment with the code - it's your fork!
- Share your improvements with the community via pull requests

---

**Remember**: This is YOUR fork. Customize it however you see fit for your needs!
