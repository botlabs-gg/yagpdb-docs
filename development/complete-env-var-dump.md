# Complete env var dump

**People with this role on the main server has bot admin status** \(number, default: 0\)   
YAGPDB\_ADMIN\_ROLE

**Channel to pull announcements from and display on the control panel homepage** \(number, default: 0\)   
YAGPDB\_ANNOUNCEMENTS\_CHANNEL

**AYLIEN App ID** \(string\)   
YAGPDB\_AYLIENAPPID

**AYLIEN App Key** \(string\)   
YAGPDB\_AYLIENAPPKEY

**Backgroundn worker http server address** \(string, default: localhost:5004\)   
YAGPDB\_BGWORKER\_HTTP\_SERVER\_ADDR

**Channel to log added/left servers to** \(number, default: 0\)   
YAGPDB\_BOTLEAVESJOINS

**botrest listening address, it will use the first port available above 5010** \(string, default: 127.0.0.1\)   
YAGPDB\_BOTREST\_LISTEN\_ADDRESS

**Token of the bot user**   
YAGPDB\_BOTTOKEN

**Client ID of the discord application**   
YAGPDB\_CLIENTID

**Client Secret of the discord application**   
YAGPDB\_CLIENTSECRET

**Gateway connection logging channel** \(number, default: 0\)   
YAGPDB\_CONNEVT\_CHANNEL

**Gateway connection status channel** \(number, default: 0\)   
YAGPDB\_CONNSTATUS\_CHANNEL

**Disables keepalive connections for outgoing requests to discord, this shouldn't be needed but i had networking issues once so i had to** \(true/false, default: false\)   
YAGPDB\_DISABLE\_KEEPALIVES

**Disable logging of http requests to web server** \(true/false, default: false\)   
YAGPDB\_DISABLE\_REQUEST\_LOGGING

**dogstatsd address** \(string\)   
YAGPDB\_DOGSTATSDADDRESS

**Email used when fetching lets encrypt certificate** \(string\)   
YAGPDB\_EMAIL

**Google analytics id** \(string\)   
YAGPDB\_GA\_ID

**Google reCAPTCHA site secret** \(string\)   
YAGPDB\_GOOGLE\_RECAPTCHA\_SECRET

**Google reCAPTCHA site key** \(string\)   
YAGPDB\_GOOGLE\_RECAPTCHA\_SITE\_KEY

**Google safebrowsing API Key** \(string\)   
YAGPDB\_GOOGLE\_SAFEBROWSING\_API\_KEY

**Host without the protocol, example: example.com, used by the webserver**   
YAGPDB\_HOST

**Main server used for various purposes, like assigning people with a certain role as bot admins** \(number, default: 0\)   
YAGPDB\_MAIN\_SERVER

**Maximum number of concurrent outgoing requests to discord** \(number, default: 25\)   
YAGPDB\_MAX\_CCR

**Enable the memory monitor, will attempt to free resources when os is running low** \(true/false, default: true\)   
YAGPDB\_MEM\_MONITOR\_ENABLED

**Sharding orchestrator address to connect to, if set it will be put into orchstration mode** \(string\)   
YAGPDB\_ORCHESTRATOR\_ADDRESS

**ID of the owner of the bot**   
YAGPDB\_OWNER

**Access token for the patreon integration** \(string\)   
YAGPDB\_PATREON\_API\_ACCESS\_TOKEN

**Client id for the patreon integration** \(string\)   
YAGPDB\_PATREON\_API\_CLIENT\_ID

**Client secret for the patreon integration** \(string\)   
YAGPDB\_PATREON\_API\_CLIENT\_SECRET

**Refresh token for the patreon integration** \(string\)   
YAGPDB\_PATREON\_API\_REFRESH\_TOKEN

**Postgres database** \(string, default: yagpdb\)   
YAGPDB\_PQDB

**Postgres host** \(string, default: localhost\)   
YAGPDB\_PQHOST

**Postgres passoword** \(string\)   
YAGPDB\_PQPASSWORD

**Postgres user** \(string, default: postgres\)   
YAGPDB\_PQUSERNAME

**People with this role on the main server has global read only access to configs** \(number, default: 0\)   
YAGPDB\_READONLY\_ACCESS\_ROLE

**Client ID for the reddit api application** \(string\)   
YAGPDB\_REDDIT\_CLIENTID

**Client Secret for the reddit api application** \(string\)   
YAGPDB\_REDDIT\_CLIENTSECRET

**Redirect URI for the reddit api application** \(string\)   
YAGPDB\_REDDIT\_REDIRECT

**RefreshToken for the reddit api application, you need to ackquire this manually, should be set to permanent** \(string\)   
YAGPDB\_REDDIT\_REFRESHTOKEN

**Redis address** \(string, default: localhost:6379\)   
YAGPDB\_REDIS

**Disable reaction removal in single mode, could be heavy on number of requests** \(true/false, default: false\)   
YAGPDB\_ROLECOMMANDS\_DISABLE\_REACTION\_REMOVAL\_SINGLE\_MODE

**Sentry credentials for sentry logging hook**   
YAGPDB\_SENTRY\_DSN

**Twitter access token** \(string\)   
YAGPDB\_TWITTER\_ACCESS\_TOKEN

**Twitter access token secret** \(string\)   
YAGPDB\_TWITTER\_ACCESS\_TOKEN\_SECRET

**Twitter consumer key** \(string\)   
YAGPDB\_TWITTER\_CONSUMER\_KEY

**Twitter consumer secret** \(string\)   
YAGPDB\_TWITTER\_CONSUMER\_SECRET

**If were behind a reverse proxy, this is the header field with the real ip that the proxy passes along** \(string\)   
YAGPDB\_WEB\_REVERSE\_PROXY\_CLIENT\_IP\_HEADER

**Youtube websub push verify token, set it to a random string and never change it** \(string, default: asdkpoasdkpaoksdpako\)   
YAGPDB\_YOUTUBE\_VERIFY\_TOKEN

**Ad Height** \(number, default: 0\)   
YAGPDB\_AD\_H

**The ad image**  \(string\)   
YAGPDB\_AD\_IMG\_PATH

**Link to follow when clicking on the ad** \(string\)   
YAGPDB\_AD\_LINK

**Comma seperated list of video paths in different formats** \(string\)   
YAGPDB\_AD\_VIDEO\_PATHS

**Ad width** \(number, default: 0\)   
YAGPDB\_AD\_W

