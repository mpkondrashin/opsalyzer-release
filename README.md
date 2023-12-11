# Opswat to Trend Micro Sandbox Integration Utility

**Opsalyzer provides ability to integrate Deep Discovery Analyzer or Vision One cloud sandbox service as External Scanner to Opswat MetaDefender Core**

## Installation

1. Download [latest release](https://github.com/mpkondrashin/opsalyzer-release/releases/latest) for your platform. 
1. Unpack archive contents to any folder on Opswat server.
1. Pick what kind of sandbox to use: Deep Discovery Analyzer or Vision One Cloud Sandbox service
1. For using Deep Discovery Analyzer
    1. Pick [UUID](https://www.uuidgenerator.net/) for your Opsalyzer installation.
    1. Create ```config.json``` file with minimal contents (see below)
1. For using Vision One Cloud Sandbox service create ```config.json``` with minimal contents (see below)
1. Add path to opsalyzer executables as external scanner using Opswat Web console.
1. Check one file manually.
1. Check opsaluzer.log file for successful submission event.
1. Remove "log_level" and "log_file" lines from ```config.json```.
1. Optionally, add Periculosum to avoid submitting unsupported files (see next session).

Minimal configuration for using Deep Discovery Analyzer:
```json
{
    "analyzer": "<analyzer address>",
    "api_key": "<analyzer api key - from menu Help -> About",
    "ignore_tls_errors": true,
    "only_cached": true,
    "client_id": "<generated UUID>",
    "log_level": 2,
    "log_file": "opsalizer.log",
    "accept_high_risk": false,
    "accept_medium_risk": false,
    "accept_low_risk": false,
    "accept_error": true,
    "accept_timeout": true,
    "version": "1.8",
}
```

Minimal configuration for using Vision One sandbox service:
```json
{
    "address": "api.<your region>.xdr.trendmicro.com"
    "token": "<generate token using Vision One console>" 
    "only_cached": true,
    "log_level": 2,
    "log_file": "opsalizer.log",
    "accept_high_risk": false,
    "accept_medium_risk": false,
    "accept_low_risk": false,
    "accept_error": true,
    "accept_timeout": true,
}
```

## Periculosum Integration

To reduce amount of not supported files submitted to Deep Discovery Analyzer, (Periculosum)[https://github.com/mpkondrashin/periculosum] project can be used.
To use Periculosum, just download (latest version)[https://github.com/mpkondrashin/periculosum/releases/latest] and unpack its content to same folder as opsalyzer executable.

**Note:** Put all unpacked files into the same folder as opsalyzer executable and not into subfolder.

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
|String|max_file_size<br/>--max_file_size<br/>OPSAL_MAX_FILE_SIZE|maximum file size|50MB|
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
|Duration|connection_timeout<br/>--connection_timeout<br/>OPSAL_CONNECTION_TIMEOUT|Connection timeout for Web API connections|15s|
|String|version<br/>--version<br/>OPSAL_VERSION|Force Web Services API version (only if Analyzer used)|2.0|
|String|--config<br/>OPSAL_CONFIG|Provide alternative configuration file path|none|


## Configuration file sample

Sample of configuration file:
```json
{
    "analyzer": "1.2.3.4",
    "api_key": "12341234-1234-1234-1234-213412341234",
    "max_file_size": "25MB",
    "ignore_tls_errors": true,
    "timeout": "5m",
    "only_cached": false,
    "pull_interval": "10s",
    "client_id": "12341234-1234-1234-1234-213412341234",
    "client_id_folder": ".",
    "address": "api.eu.xdr.trendmicro.com",
    "token": "abcde...",
    "log_level": 2,
    "log_file": "opsalizer.log",
    "accept_high_risk": false,
    "accept_medium_risk": false,
    "accept_low_risk": false,
    "accept_error": false,
    "accept_timeout": true,
    "connection_timeout": "30s",
    "version": "1.8",
}
```

**Note #1:** Do not use this configuration "as is". Please use minimal number of the required options removing the rest to use default values (see examples above)

**Note #2:** Changing configuration file does not require any Opswat reconfiguration or restart. Next analyzed file will use updated configuration.

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
