# Carbon Mapper Platform API Tutorials

Tutorials offer information for and examples of working with [Carbon Mapper](https://carbonmapper.org/)'s
[platform API](https://api.carbonmapper.org/). Refer to the
[platform API documentation](https://api.carbonmapper.org/api/v1/docs) for technical API details.

# Using the Tutorials

## Installing Jupyter Notebook

Refer to Jupyter's official [Installing Jupyter](https://jupyter.org/install) page for information about installing
Jupyter Notebook. A virtual environment may be required before installation, depending on the platform Notebook is
installed to. Refer to the official Python documentation for
[creating virtual environments](https://docs.python.org/3/library/venv.html#creating-virtual-environments).

## Accessing the tutorials

From within the _platform_public_ project root directory, run `jupyter notebook`:

```bash
# Activate the virtual environment if required
user@hostname:./platform_public$ source <venv_dir>/bin/activate
user@hostname:./platform_public$ jupyter notebook
```

# API Authentication

Many platform API endpoints require authentication. Some endpoints may return different results depending on
authentication status and the token's scopes. A platform account is required to obtain an API access token. Users
without accounts are encouraged to [register](https://platform.carbonmapper.org/account/register/) for an account.

## Obtaining a Scoped Token Using the Platform Website

A scoped token can be generated  by logging in to the [platform application](https://platform.carbonmapper.org/) and
visiting the [API Tokens](https://platform.carbonmapper.org/account/tokens/) section of their Account page. The token
will only be displayed to the user once, upon generation. If generating the token for future use, it should be stored
securely and should not be committed to code repositories.

## Obtaining a Scoped Token Using the Platform API

Refer to the [scoped token tutorial](scoped_token.ipynb).
