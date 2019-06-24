# Complete enviroment variable list

<table>
  <thead>
    <tr>
      <th style="text-align:center">Function/Usage</th>
      <th style="text-align:center">Variable</th>
      <th style="text-align:center">Default</th>
      <th style="text-align:center">Type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:center">Bot admin status</td>
      <td style="text-align:center">YAGPDB_ADMIN_ROLE</td>
      <td style="text-align:center">0</td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Source of announcements for the homepage</td>
      <td style="text-align:center">YAGPDB_ANNOUNCEMENTS_CHANNEL</td>
      <td style="text-align:center">0</td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">AYLIEN app ID</td>
      <td style="text-align:center">YAGPDB_AYLIENAPPID</td>
      <td style="text-align:center">&lt;del&gt;&lt;/del&gt;</td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">AYLIEN app key</td>
      <td style="text-align:center">YAGPDB_AYLIENAPPKEY</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Background worker listen address</td>
      <td style="text-align:center">YAGPDB_BGWORKER_HTTP_SERVER_ADDR</td>
      <td style="text-align:center">localhost:5004</td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Log channel for join/leave events</td>
      <td style="text-align:center">YAGPDB_BOTLEAVESJOINS</td>
      <td style="text-align:center">0</td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Botrest listen adress</td>
      <td style="text-align:center">YAGPDB_BOTREST_LISTEN_ADDRESS</td>
      <td style="text-align:center">
        <p>127.0.0.1</p>
        <p>(port 5010 or the next higher available port)</p>
      </td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Access token for the bot</td>
      <td style="text-align:center">YAGPDB_BOTTOKEN</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Client ID for the Discord application</td>
      <td style="text-align:center">YAGPDB_CLIENTID</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Client secret for the Discord application</td>
      <td style="text-align:center">YAGPDB_CLIENTSECRET</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Gateway events log channel</td>
      <td style="text-align:center">YAGPDB_CONNEVT_CHANNEL</td>
      <td style="text-align:center">0</td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Gateway connection status channel</td>
      <td style="text-align:center">YAGPDB_CONNSTATUS_CHANNEL</td>
      <td style="text-align:center">0</td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Disable keepalive connections to Discord [1]</td>
      <td style="text-align:center">YAGPDB_DISABLE_KEEPALIVES</td>
      <td style="text-align:center">false</td>
      <td style="text-align:center">boolean</td>
    </tr>
    <tr>
      <td style="text-align:center">Disable logging of http requests</td>
      <td style="text-align:center">YAGPDB_DISABLE_REQUEST_LOGGING</td>
      <td style="text-align:center">false</td>
      <td style="text-align:center">boolean</td>
    </tr>
    <tr>
      <td style="text-align:center">Datadog statsd collector adress</td>
      <td style="text-align:center">YAGPDB_DOGSTATSDADDRESS</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Let&apos;s Encrypt certificate email [2]</td>
      <td style="text-align:center">YAGPDB_EMAIL</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Google analytics ID</td>
      <td style="text-align:center">YAGPDB_GA_ID</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">reCAPTCHA secret</td>
      <td style="text-align:center">YAGPDB_GOOGLE_RECAPTCHA_SECRET</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">reCAPTCHA key</td>
      <td style="text-align:center">YAGPDB_GOOGLE_RECAPTCHA_SITE_KEY</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Google safebrowing API key</td>
      <td style="text-align:center">YAGPDB_GOOGLE_SAFEBROWSING_API_KEY</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Server hostname</td>
      <td style="text-align:center">YAGPDB_HOST</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Main server ID [3]</td>
      <td style="text-align:center">YAGPDB_MAIN_SERVE</td>
      <td style="text-align:center">0</td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Maximum concurrent requests to Discord</td>
      <td style="text-align:center">YAGPDB_MAX_CCR</td>
      <td style="text-align:center">25</td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Memory monitor [4]</td>
      <td style="text-align:center">YAGPDB_MEM_MONITOR_ENABLED</td>
      <td style="text-align:center">true</td>
      <td style="text-align:center">boolean</td>
    </tr>
    <tr>
      <td style="text-align:center">Sharding orchestrator adress [5]</td>
      <td style="text-align:center">YAGPDB_ORCHESTRATOR_ADDRESS</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Discord ID of the bot owner</td>
      <td style="text-align:center">YAGPDB_OWNER</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Patreon API access token</td>
      <td style="text-align:center">YAGPDB_PATREON_API_ACCESS_TOKEN</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Patreon API client id</td>
      <td style="text-align:center">YAGPDB_PATREON_API_CLIENT_ID</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Pateron API client secret</td>
      <td style="text-align:center">YAGPDB_PATREON_API_CLIENT_SECRET</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Patreon API refresh token</td>
      <td style="text-align:center">YAGPDB_PATREON_API_REFRESH_TOKEN</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Posgres database</td>
      <td style="text-align:center">YAGPDB_PQDB</td>
      <td style="text-align:center">yagpdb</td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Postgres host</td>
      <td style="text-align:center">YAGPDB_PQHOST</td>
      <td style="text-align:center">localhost</td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Postgres password</td>
      <td style="text-align:center">YAGPDB_PQPASSWORD</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Postgres user</td>
      <td style="text-align:center">YAGPDB_PQUSERNAME</td>
      <td style="text-align:center">postgres</td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Role with global read only configuration access</td>
      <td style="text-align:center">YAGPDB_READONLY_ACCESS_ROLE</td>
      <td style="text-align:center">0</td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Reddit API client ID</td>
      <td style="text-align:center">YAGPDB_REDDIT_CLIENTID</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Reddit API client secret</td>
      <td style="text-align:center">YAGPDB_REDDIT_CLIENTSECRET</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Redirect URI for Reddit app</td>
      <td style="text-align:center">YAGPDB_REDDIT_REDIRECT</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">RefreshToken for Reddit API</td>
      <td style="text-align:center">YAGPDB_REDDIT_REFRESHTOKEN</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Redis adress</td>
      <td style="text-align:center">YAGPDB_REDIS</td>
      <td style="text-align:center">localhost:6379</td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Reaction removal in single mode disable [6]</td>
      <td style="text-align:center">YAGPDB_ROLECOMMANDS_DISABLE_REACTION_REMOVAL_SINGLE_MODE</td>
      <td style="text-align:center">false</td>
      <td style="text-align:center">boolean</td>
    </tr>
    <tr>
      <td style="text-align:center">Sentry credentials for logging hook</td>
      <td style="text-align:center">YAGPDB_SENTRY_DSN</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Twitter API access token</td>
      <td style="text-align:center">YAGPDB_TWITTER_ACCESS_TOKEN</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Twitter API secret</td>
      <td style="text-align:center">YAGPDB_TWITTER_ACCESS_TOKEN_SECRET</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Twitter consumer key</td>
      <td style="text-align:center">YAGPDB_TWITTER_CONSUMER_KEY</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Twitter consumer secret</td>
      <td style="text-align:center">YAGPDB_TWITTER_CONSUMER_SECRET</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Reverse Proxy Real IP header</td>
      <td style="text-align:center">YAGPDB_WEB_REVERSE_PROXY_CLIENT_IP_HEADER</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">YouTube websub push verify token [7]</td>
      <td style="text-align:center">YAGPDB_YOUTUBE_VERIFY_TOKEN</td>
      <td style="text-align:center">asdkpoasdkpaoksdpako</td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Ad height</td>
      <td style="text-align:center">YAGPDB_AD_H</td>
      <td style="text-align:center">0</td>
      <td style="text-align:center">integer</td>
    </tr>
    <tr>
      <td style="text-align:center">Ad image path</td>
      <td style="text-align:center">YAGPDB_AD_IMG_PATH</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Ad follow link</td>
      <td style="text-align:center">YAGPDB_AD_LINK</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Ad video paths</td>
      <td style="text-align:center">YAGPDB_AD_VIDEO_PATHS</td>
      <td style="text-align:center"></td>
      <td style="text-align:center">string</td>
    </tr>
    <tr>
      <td style="text-align:center">Ad width</td>
      <td style="text-align:center">YAGPDB_AD_W</td>
      <td style="text-align:center">0</td>
      <td style="text-align:center">integer</td>
    </tr>
  </tbody>
</table>\[1\] known to help against network issues  
\[2\] ****only when using Let's Encrypt companion  
****\[3\] grants certain roles bot admin access  
\[4\] will free resources when running low  
\[5\] will put the bot into orchestration mode  
\[6\] leaving it enabled could cause a big amount of requests  
\[7\] should be set to somthing random and never change  
\[8\] should be comma separated paths  


