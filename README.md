
# Opswat to Deep Discovery Analuyzer Integration Application

**Opsalyzer provides ability to integrate Deep Discovery Analyzer as External Scanner to Opswat MetaDefender Core**

## Options

Opsalyzer provides following ways to provide options:
1. Configuration file config.json. Application seeks for this file in its current folder
2. Environment variables
3. Command line parameters

Following options are available:

| Type | JSON Option<br/>Command line<br/>Env Variable | Description | Default |
| ---- | --------------------------------------------- | ----------- | ------- |
|String|analyzer<br/>--analyzer<br/>OPSAL_ANALYZER|Analyzer address|none|
|String|api_key<br/>--api_key<br/>OPSAL_API_KEY|Analyzer API key|none|
|Integer|max_file_size<br/>--max_file_size<br/>OPSAL_MAX_FILE_SIZE|maximum file size|50MB|
|Boolean|ignore_tls_errors<br/>--ignore_tls_errors<br/>OPSAL_IGNORE_TLS_ERRORS|ignore TLS errors|false|
|Duration|timeout<br/>--timeout<br/>OPSAL_TIMEOUT|file analysis timeout|20m|
|Boolean|only_cached<br/>--only_cached<br/>OPSAL_ONLY_CACHED|do not wait from analysis result. Only check Analyzer cache|false|
|Duration|pull_interval<br/>--pull_interval<br/>OPSAL_PULL_INTERVAL|iterval to check file analysis result|1m|
|String|client_id<br/>--client_id<br/>OPSAL_CLIENT_ID|Client ID for Analyzer (is generated automatically if missing)|none|
|String|client_id_folder<br/>--client_id_folder<br/>OPSAL_CLIENT_ID_FOLDER|Folder for Client ID file (defaults to current folder for opsalyzer process)|.|
|Integer|log_level<br/>--log_level<br/>OPSAL_LOG_LEVEL|Log level 0-none, 1-warnings, 2-info, 3-debug|0|
|String|log_file<br/>--log_file<br/>OPSAL_LOG_FILE|filename to write log|none|
|Boolean|accept_high_risk<br/>--accept_high_risk<br/>OPSAL_ACCEPT_HIGH_RISK|files detected as high risk are trated as non malicious|false|
|Boolean|accept_medium_risk<br/>--accept_medium_risk<br/>OPSAL_ACCEPT_MEDIUM_RISK|files detected as medium risk are trated as non malicious|false|
|Boolean|accept_low_risk<br/>--accept_low_risk<br/>OPSAL_ACCEPT_LOW_RISK|files detected as low risk are trated as non malicious|false|
|Boolean|accept_error<br/>--accept_error<br/>OPSAL_ACCEPT_ERROR|files that resulted error during analysis are trated as non malicious|false|
|Boolean|accept_timeout<br/>--accept_timeout<br/>OPSAL_ACCEPT_TIMEOUT|files that resulted timeout during analysis are trated as non malicious|false|


## Return Codes

If Opsalyzer successfuly finishes sample analysis it returnes code 0 and result is printed to Stdout. In case of
error, non zero Return Code can be checked to diagnose a problem.

| Return Code | Description |
| ----------- | ----------- |
|0|Ok|
|1|Viper bind p flags error|
|2|Command line error|
|3|Config read error|
|4|Open log error|
|5|Get hostname failed|
|6|Analyzer url format error|
|7|Read stdin error|
|8|Input json format error|
|9|Read client id file|
|10|Write client id file|
|11|Missing url|
|12|Missing api key|
|13|Api key format error|
|14|Failed to upload sample|
|15|Fail check duplicate sample|
|16|Register failed|
|17|Fail second check duplicate sample|
|18|Sample not found|
|19|Sample analysis error|
|20|Sample analysis timeout|
|21|Unexpected status returned|
|22|Output marshal error|


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
