
# Opswat to Deep Discovery Analyzer Integration Application

**Opsalyzer provides ability to integrate Deep Discovery Analyzer as External Scanner to Opswat MetaDefender Core**

## Options

Opsalyzer provides following ways to provide options:
1. Configuration file config.json. Application seeks for this file in its current folder
2. Environment variables
3. Command line parameters

Following options are available:

| Type | JSON Option<br/>Command line<br/>Env Variable | Description | Default |
| ---- | --------------------------------------------- | ----------- | ------- |
|String|analyzer<br/>--analyzer<br/>OPSAL_ANALYZER|Analyzer address (only if Analyzer used)|none|
|String|api_key<br/>--api_key<br/>OPSAL_API_KEY|Analyzer API key (only if Analyzer used)|none|
|Integer|max_file_size<br/>--max_file_size<br/>OPSAL_MAX_FILE_SIZE|maximum file size|50MB|
|Boolean|ignore_tls_errors<br/>--ignore_tls_errors<br/>OPSAL_IGNORE_TLS_ERRORS|ignore TLS errors. (only if Analyzer used)|false|
|Duration|timeout<br/>--timeout<br/>OPSAL_TIMEOUT|file analysis timeout|20m|
|Boolean|only_cached<br/>--only_cached<br/>OPSAL_ONLY_CACHED|do not wait from analysis result. Only check Analyzer cache|false|
|Duration|pull_interval<br/>--pull_interval<br/>OPSAL_PULL_INTERVAL|iterval to check file analysis result|1m|
|String|client_id<br/>--client_id<br/>OPSAL_CLIENT_ID|Client ID for Analyzer. It is generated automatically if missing. (only if Analyzer used)|none|
|String|client_id_folder<br/>--client_id_folder<br/>OPSAL_CLIENT_ID_FOLDER|Folder for Client ID file. It defaults to current folder for opsalyzer process. (only if Analyzer used)|.|
|String|address<br/>--address<br/>OPSAL_ADDRESS|Vision One address (only if Vision One Sandbox is used)|none|
|String|token<br/>--token<br/>OPSAL_TOKEN|Vision One token (only if Vision One Sandbox is used)|none|
|Integer|log_level<br/>--log_level<br/>OPSAL_LOG_LEVEL|Log level 0-none, 1-warnings, 2-info, 3-debug|0|
|String|log_file<br/>--log_file<br/>OPSAL_LOG_FILE|filename to write log|none|
|Boolean|accept_high_risk<br/>--accept_high_risk<br/>OPSAL_ACCEPT_HIGH_RISK|files detected as high risk are trated as non malicious|false|
|Boolean|accept_medium_risk<br/>--accept_medium_risk<br/>OPSAL_ACCEPT_MEDIUM_RISK|files detected as medium risk are trated as non malicious|false|
|Boolean|accept_low_risk<br/>--accept_low_risk<br/>OPSAL_ACCEPT_LOW_RISK|files detected as low risk are trated as non malicious|false|
|Boolean|accept_error<br/>--accept_error<br/>OPSAL_ACCEPT_ERROR|files that resulted error during analysis are trated as non malicious|false|
|Boolean|accept_timeout<br/>--accept_timeout<br/>OPSAL_ACCEPT_TIMEOUT|files that resulted timeout during analysis are trated as non malicious|false|
|Duration|connection_timeout<br/>--connection_timeout<br/>OPSAL_CONNECTION_TIMEOUT|Connection timeout|15s|
|String|version<br/>--version<br/>OPSAL_VERSION|Force Web Services API version|2.0|
|String|config<br/>--config<br/>OPSAL_CONFIG|Configuration file path|none|


## Return Codes

If Opsalyzer successfuly finishes sample analysis it returnes code 0 and result is printed to Stdout. In case of
error, non zero Return Code can be checked to diagnose a problem.

| Return Code | Description |
| ----------- | ----------- |
|0|Ok|
|1|Viper bind p flags error|
|2|Program crash|
|3|Command line error|
|4|Config read error|
|5|Open log error|
|6|Get hostname failed|
|7|Analyzer url format error|
|8|Read stdin error|
|9|Input json format error|
|10|Read client id file|
|11|Write client id file|
|12|Missing url|
|13|Missing api key|
|14|Api key format error|
|15|Failed to upload sample|
|16|Fail check duplicate sample|
|17|Register failed|
|18|Fail second check duplicate sample|
|19|Sample not found|
|20|Sample analysis error|
|21|Sample analysis timeout|
|22|Get brief report error|
|23|Unexpected status returned|
|24|Output marshal error|
|25|Get opsalyzer path failed|
|26|Config file missing|
|27|Read file error|
|28|Missing vision one domain|


For further diagnostics logging can be enabled.

## Logging

Logging is controlled by log_level and log_file parameters.
log_file specifies file to write log message and log_level verbosity of the log file:

- 0 - turn logging off
- 1 - log only warnings
- 2 - log general info messages also
- 3 - enable debug logging

**Warning:** log file is not limited is size anyhow, so after debugging it should be turned off.

## Opswat MetaDefender Core Configuration (TODO)
