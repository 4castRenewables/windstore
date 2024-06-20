# Upload external project data to 4cast s3 bucket

The manual assumes that 
- Access credentials have been recieved as csv from 4cast including `Access key ID` and `Secret access key`. 
- [Aws CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) is installed on local machine.
  - Confirm via calling `aws --version`.

IEE please upload the files to `path_s3=s3://windstore-weather-data/iee/`.
### Configure AWS CLI 

Use the option `--profile <profile_name>` to set up access keys for the accounts.
See https://docs.aws.amazon.com/cli/latest/userguide/cli-authentication-user.html for more details.

The profile will be saved in your `~/.aws` folder in two files `config` and `credentials`. The former contains the profile, the latter the related  AWS Access Key ID and AWS Secret Access Key. `config` is 

```
[default]
region = eu-central-1
output = json

[profile <profile_name>]
region = eu-central-1
output = json
```

When adding this new profile `<profile_name>`, make sure to also add new `credentials` in `~/.aws/credentials` (keys may agree).

```
[default]
aws_access_key_id = <AWS_ACCESS_KEY_ID>
aws_secret_access_key = <AWS_SECRET_ACCESS_KEY>

[<profile_name>]
aws_access_key_id = <AWS_ACCESS_KEY_ID>
aws_secret_access_key = <AWS_SECTRET_ACCESS_KEY>
```

### Use AWS CLI to upload files

After configuration, the provided target s3 path should be accessible. To test, call

```bash
aws --profile <profile_name> s3 ls <path_s3> --recursive
```

Uploading files can be done via

```bash
aws --profile windstore-datasender s3 cp <local_path_to_folder> <path_s3> --recursive
```

Make sure that `path_s3` is set correctly as uploading should only be possible to the specified "sub-directory"! 