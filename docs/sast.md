# SAST: Static Application Security Testing

**NOTE**
This is specific to the language - GitLab provides a list of tools that can be used for various languages
[List of languages and frameworks](https://docs.gitlab.com/ee/user/application_security/sast/index.html#supported-languages-and-frameworks)

Since the appliation we're using is Ruby on Rails we'll be using [Brakeman](https://brakemanscanner.org)

## Brakeman

Brakeman is pretty simple to use, for boolio-api

```bash
# from application directory run
brakeman
```

So lets add this to our `gitlab-ci.yml` file.

```yaml
# .gitlab-ci.yml
# ...

"SAST":
  stage: test
  image: $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA
  script:
    - gem install brakeman
    - brakeman

# ...
```

When an error is detected
```
== Brakeman Report ==

Application Path: /app
Rails Version: 5.2.0
Brakeman Version: 4.5.1
Scan Date: 2019-06-18 03:55:26 +0000
Duration: 0.126419906 seconds
Checks Run: BasicAuth, BasicAuthTimingAttack, ContentTag, CreateWith, CrossSiteScripting, DefaultRoutes, Deserialize, DetailedExceptions, DigestDoS, DynamicFinders, EscapeFunction, Evaluation, Execute, FileAccess, FileDisclosure, FilterSkipping, ForgerySetting, HeaderDoS, I18nXSS, JRubyXML, JSONEncoding, JSONParsing, LinkTo, LinkToHref, MailTo, MassAssignment, MimeTypeDoS, ModelAttrAccessible, ModelAttributes, ModelSerialize, NestedAttributes, NestedAttributesBypass, NumberToCurrency, PermitAttributes, QuoteTableName, Redirect, RegexDoS, Render, RenderDoS, RenderInline, ResponseSplitting, RouteDoS, SQL, SQLCVEs, SSLVerify, SafeBufferManipulation, SanitizeMethods, SelectTag, SelectVulnerability, Send, SendFile, SessionManipulation, SessionSettings, SimpleFormat, SingleQuotes, SkipBeforeFilter, SprocketsPathTraversal, StripTags, SymbolDoSCVE, TranslateBug, UnsafeReflection, ValidationRegex, WithoutProtection, XMLDoS, YAMLParsing

== Overview ==

Controllers: 2
Models: 2
Templates: 1
Errors: 0
Security Warnings: 1

== Warning Types ==

Path Traversal: 1

== Warnings ==

Confidence: High
Category: Path Traversal
Check: SprocketsPathTraversal
Message: sprockets 3.7.1 has a path traversal vulnerability (CVE-2018-3760). Upgrade to sprockets 3.7.2 or newer
File: Gemfile.lock
Line: 116
```

When everything is good to go

```
== Brakeman Report ==

Application Path: /app
Rails Version: 5.2.3
Brakeman Version: 4.5.1
Scan Date: 2019-06-18 05:12:10 +0000
Duration: 0.113738602 seconds
Checks Run: BasicAuth, BasicAuthTimingAttack, ContentTag, CreateWith, CrossSiteScripting, DefaultRoutes, Deserialize, DetailedExceptions, DigestDoS, DynamicFinders, EscapeFunction, Evaluation, Execute, FileAccess, FileDisclosure, FilterSkipping, ForgerySetting, HeaderDoS, I18nXSS, JRubyXML, JSONEncoding, JSONParsing, LinkTo, LinkToHref, MailTo, MassAssignment, MimeTypeDoS, ModelAttrAccessible, ModelAttributes, ModelSerialize, NestedAttributes, NestedAttributesBypass, NumberToCurrency, PermitAttributes, QuoteTableName, Redirect, RegexDoS, Render, RenderDoS, RenderInline, ResponseSplitting, RouteDoS, SQL, SQLCVEs, SSLVerify, SafeBufferManipulation, SanitizeMethods, SelectTag, SelectVulnerability, Send, SendFile, SessionManipulation, SessionSettings, SimpleFormat, SingleQuotes, SkipBeforeFilter, SprocketsPathTraversal, StripTags, SymbolDoSCVE, TranslateBug, UnsafeReflection, ValidationRegex, WithoutProtection, XMLDoS, YAMLParsing

== Overview ==

Controllers: 2
Models: 2
Templates: 1
Errors: 0
Security Warnings: 0

== Warning Types ==


No warnings found
```

NOTES:
- https://docs.gitlab.com/ee/user/application_security/sast/index.html
- https://brakemanscanner.org/
