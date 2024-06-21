# Carbon Mapper Platform API Tutorials

Tutorials offer information for and examples of working with [Carbon Mapper](https://carbonmapper.org/)'s platform API.
Refer to the [platform API documentation](https://api.platform.carbonmapper.org/api/v1/docs) for technical API details.

# Using the Tutorials

```bash
# Create a virtual environment
python3 -m venv .venv
# Activate the virtual environment
source .venv/bin/activate
# Install requirements
pip install -r requirements.txt
# Run Jupyter
jupyter notebook
```

# API Authentication

Many platform API endpoints require authentication. Some endpoints may return different results depending on
authentication status. Users with platform accounts can generate tokens by logging in to
the [platform application](https://platform.carbonmapper.org/) and visiting the
[API Tokens](https://platform.carbonmapper.org/account/tokens/) section of their Account page. Users without accounts
are encouraged to [register](https://platform.carbonmapper.org/account/register/) for an account.
