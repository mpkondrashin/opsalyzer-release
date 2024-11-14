# Opswat to Trend Micro Sandbox Integration Utility

![Opsalyzer Logo](opsalyzer_logo.jpg)


**Opsalyzer provides ability to integrate Deep Discovery Analyzer or Vision One cloud sandbox service as External Scanner to Opswat MetaDefender Core**

## Installation

1. Download [latest release](https://github.com/mpkondrashin/opsalyzer-release/releases/latest) for your platform. 
1. Unpack archive contents to any folder on Opswat server, i.e. ```C:\Opsalyzer```.
1. Pick what kind of sandbox to use: Deep Discovery Analyzer or Vision One Cloud Sandbox service
1. Create ```config.json``` file with minimal contents (see below)
1. Add path to opsalyzer executables as [external scanner](https://docs.opswat.com/mdcore/configuration/external-scanners-and-post-actions) using Opswat Web console. 
1. For testing: Check one file manually.
1. Check opsaluzer.log file for successful submission event.
1. Remove "log_level" and "log_file" lines from ```config.json```.
1. Optionally, add Periculosum to avoid submitting unsupported files (see next session).

Minimal configuration for using Deep Discovery Analyzer:
```yaml
analyzer:
  address: <analyzer address>,
  api_key: <analyzer api key - from menu Help -> About>
  ignore_tls_errors: true
log:
  keep: 3
  level: 2
  file: opsalyzer.log
  max_size: 100000
accept:
  medium_risk: false
  low_risk: false
  error: true
  timeout: true
  big_file: true
  high_risk: false
engine: analyzer
only_cached: true
```

Minimal configuration for using Vision One sandbox service:
```yaml
vone:
  domain: api.<your region>.xdr.trendmicro.com
  token: "<generate token using Vision One console>" 
log:
  keep: 3
  level: 2
  file: opsalyzer.log
  max_size: 100000
accept:
  medium_risk: false
  low_risk: false
  error: true
  timeout: true
  big_file: true
  high_risk: false
engine: analyzer
only_cached: true
```

## Periculosum Integration

To reduce amount of not supported files submitted to Deep Discovery Analyzer, [Periculosum](https://github.com/mpkondrashin/periculosum) project can be used.
To use Periculosum, just download [latest version](https://github.com/mpkondrashin/periculosum/releases/latest) and unpack its content to same folder as opsalyzer executable.

**Note:** Put all unpacked files into the same folder as opsalyzer executable and not into subfolder.

## Options

Opsalyzer provides following ways to provide options:
1. Configuration file config.yaml. Application seeks for this file in its current folder
2. Environment variables
3. Command line parameters

Following options are available:

| Type | JSON Option<br/>Command line<br/>Env Variable | Description | Default |
| ---- | --------------------------------------------- | ----------- | ------- |
|String|engine<br/>--engine<br/>OPSAL_ENGINE|Scan engine: Analyzer, VisionOne|none|
|String|analyzer.address<br/>--analyzer.address<br/>OPSAL_ANALYZER.ADDRESS|Analyzer URL (only if Analyzer used). Should be in form https://&lt;address&gt;|none|
|String|analyzer.api_key<br/>--analyzer.api_key<br/>OPSAL_ANALYZER.API_KEY|Analyzer API key (only if Analyzer used)|none|
|String|analyzer.max_file_size<br/>--analyzer.max_file_size<br/>OPSAL_ANALYZER.MAX_FILE_SIZE|maximum file size (should be less or equal to the limit of Analyzer/Vision One)|50MB|
|Boolean|analyzer.ignore_tls_errors<br/>--analyzer.ignore_tls_errors<br/>OPSAL_ANALYZER.IGNORE_TLS_ERRORS|ignore TLS errors. (only if Analyzer used)|false|
|Duration|analyzer.timeout<br/>--analyzer.timeout<br/>OPSAL_ANALYZER.TIMEOUT|file analysis timeout|20m|
|Boolean|only_cached<br/>--only_cached<br/>OPSAL_ONLY_CACHED|do not wait from analysis result. Only check Analyzer/Vision One cache|false|
|Duration|analyzer.pull_interval<br/>--analyzer.pull_interval<br/>OPSAL_ANALYZER.PULL_INTERVAL|iterval to check file analysis result|1m|
|String|analyzer.client_id<br/>--analyzer.client_id<br/>OPSAL_ANALYZER.CLIENT_ID|Client ID for Analyzer. It is generated automatically if missing. (only if Analyzer used). Use same client_id to make all Opsalyzers show up on the Analyzer console as a single submitter|none|
|String|analyzer.client_id_folder<br/>--analyzer.client_id_folder<br/>OPSAL_ANALYZER.CLIENT_ID_FOLDER|Folder for Client ID file. It defaults to current folder for opsalyzer process. No need if client_id option is provided (only if Analyzer used)|none|
|String|analyzer.product_name<br/>--analyzer.product_name<br/>OPSAL_ANALYZER.PRODUCT_NAME|DDAn Product name (do not change!)|Opsalyzer|
|String|analyzer.source_id<br/>--analyzer.source_id<br/>OPSAL_ANALYZER.SOURCE_ID|DDAn Source ID (do not change!)|501|
|String|analyzer.source_name<br/>--analyzer.source_name<br/>OPSAL_ANALYZER.SOURCE_NAME|DDAn Source Name (do not change!)|Opswat|
|String|analyzer.hostname<br/>--analyzer.hostname<br/>OPSAL_ANALYZER.HOSTNAME|Hostname (do not change!)|none|
|String|analyzer.protocol_version<br/>--analyzer.protocol_version<br/>OPSAL_ANALYZER.PROTOCOL_VERSION|DDAn Protocol version (do not change!)|2.0|
|String|vone.domain<br/>--vone.domain<br/>OPSAL_VONE.DOMAIN|Vision One address (only if Vision One Sandbox is used)|none|
|String|vone.token<br/>--vone.token<br/>OPSAL_VONE.TOKEN|Vision One token (only if Vision One Sandbox is used)|none|
|Integer|log.level<br/>--log.level<br/>OPSAL_LOG.LEVEL|Log level 0-none, 1-warnings, 2-info, 3-debug|0|
|String|log.file<br/>--log.file<br/>OPSAL_LOG.FILE|filename to write log (absolute path or relative from folder where opsalyzer executable reside)|opsalyzer.log|
|Integer|log.max_size<br/>--log.max_size<br/>OPSAL_LOG.MAX_SIZE|filename to write log (absolute path or relative from folder where opsalyzer executable reside)|100000000|
|Integer|log.keep<br/>--log.keep<br/>OPSAL_LOG.KEEP|filename to write log (absolute path or relative from folder where opsalyzer executable reside)|10|
|Boolean|accept.high_risk<br/>--accept.high_risk<br/>OPSAL_ACCEPT.HIGH_RISK|files detected as high risk are trated as non malicious|false|
|Boolean|accept.medium_risk<br/>--accept.medium_risk<br/>OPSAL_ACCEPT.MEDIUM_RISK|files detected as medium risk are trated as non malicious|false|
|Boolean|accept.low_risk<br/>--accept.low_risk<br/>OPSAL_ACCEPT.LOW_RISK|files detected as low risk are trated as non malicious|false|
|Boolean|accept.error<br/>--accept.error<br/>OPSAL_ACCEPT.ERROR|files that resulted error during analysis are trated as non malicious|false|
|Boolean|accept.timeout<br/>--accept.timeout<br/>OPSAL_ACCEPT.TIMEOUT|files that resulted timeout during analysis are trated as non malicious|false|
|Boolean|accept.big_file<br/>--accept.big_file<br/>OPSAL_ACCEPT.BIG_FILE|file that are note analyzed due to their big size are trated as non malicious|true|
|Duration|connection_timeout<br/>--connection_timeout<br/>OPSAL_CONNECTION_TIMEOUT|Connection timeout for Web API connections|15s|
|String|--version<br/>OPSAL_VERSION|Force Web Services API version (only if Analyzer used)|2.0|
|String|config<br/>--config<br/>OPSAL_CONFIG|Provide alternative configuration file path|none|
|Boolean|proxy.active<br/>--proxy.active<br/>OPSAL_PROXY.ACTIVE|use proxy|false|
|String|proxy.address<br/>--proxy.address<br/>OPSAL_PROXY.ADDRESS|Proxy address|none|
|Integer|proxy.port<br/>--proxy.port<br/>OPSAL_PROXY.PORT|Proxy port|0|
|String|proxy.authtype<br/>--proxy.authtype<br/>OPSAL_PROXY.AUTHTYPE|Proxy authentication type: None, Basic, NTLM|None|
|String|proxy.username<br/>--proxy.username<br/>OPSAL_PROXY.USERNAME|Proxy username|none|
|String|proxy.password<br/>--proxy.password<br/>OPSAL_PROXY.PASSWORD|Proxy password|none|
|String|proxy.domain<br/>--proxy.domain<br/>OPSAL_PROXY.DOMAIN|NTLM auth domain|none|
|String|unsupported.folder<br/>--unsupported.folder<br/>OPSAL_UNSUPPORTED.FOLDER|folder for unsupported files|unsupported|
|Integer|unsupported.limit<br/>--unsupported.limit<br/>OPSAL_UNSUPPORTED.LIMIT|limit of unsupported files to keep. Older ones will be deleted|10|


## Configuration file sample

Sample of configuration file with all possible parameters:
```yaml
only_cached: false
vone:
  domain: api.eu.xdr.trendmicro.com
  token: abcde...
log:
  level: 2
  file: opsalyzer.log
  max_size: 100000
  keep: 3
engine: analyzer
analyzer:
  pull_interval: 10s
  client_id: 12341234-1234-1234-1234-213412341234
  source_id: 
  source_name: 
  hostname: 
  protocol_version: 1.8
  address: https://1.2.3.4
  max_file_size: 25MB
  ignore_tls_errors: true
  timeout: 5m
  client_id_folder: .
  product_name: 
  api_key: 12341234-1234-1234-1234-213412341234
accept:
  medium_risk: false
  low_risk: false
  error: true
  timeout: true
  big_file: true
  high_risk: false
connection_timeout: 30s
version: 1.8
proxy:
  domain: company.local
  active: true
  address: 10.10.10.1
  port: 3128
  authtype: NTLM
  username: michael
  password: Kr24^s_%12sa
unsupported:
  folder: unsupported
  limit: 100

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
|4|Configuration error|
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
|29|Get executable path error|
|30|Client id format error|
|31|Unknown antivirus type|


For further diagnostics logging can be enabled.

## Logging

Logging is controlled by log_level and log_file parameters.
log_file specifies file to write log message and log_level verbosity of the log file:

- 0 - turn logging off
- 1 - log only warnings
- 2 - log general info messages also
- 3 - enable debug logging

**Warning:** log file is not limited is size anyhow, so after debugging it should be turned off.
