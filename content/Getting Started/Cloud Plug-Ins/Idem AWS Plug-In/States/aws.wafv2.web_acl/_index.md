---
title: "aws.wafv2.web_acl"
weight: 20
---

{{< tabs "functions" >}}
{{< tab "absent" >}}

```
Deletes the specified WebACL.
You can only use this if ManagedByFirewallManager is false in the specified WebACL.

Args:
    name(text): The name of the web ACL. You cannot change the name of a web ACL after you create it.
    resource_id(text): AWS WAF ID. Idem automatically considers this resource being absent if this field is not specified.
    scope(text): Specifies whether this is for an Amazon CloudFront distribution or for a regional application.
        A regional application can be an Application Load Balancer (ALB), an Amazon API Gateway REST API, or an
        AppSync GraphQL API.
        To work with CloudFront, you must also specify the Region US East (N. Virginia) as follows:
        * CLI -- Specify the Region when you use the CloudFront scope: --scope=CLOUDFRONT --region=us-east-1 .
        * API and SDKs -- For all calls, use the Region endpoint us-east-1.

Request Syntax:
    [web-acl-name]::
        aws.wafv2.web_acl.absent:
        - name: 'string'
        - scope: 'string'

Examples:

    .. code-block:: sls

        demo_waf::
           aws.wafv2.web_acl.absent:
            - name: demo_waf
            - scope: REGIONAL

Returns:
    Dict[str, Any]
```
{{< /tab >}}

{{< tab "describe" >}}

```
Retrieves an WebACLSummary objects for the web ACLs that you manage.

Examples:

    .. code-block:: bash

        $ idem describe aws.wafv2.web_acl

Returns:
    Dict[str, Any]
```
{{< /tab >}}

{{< tab "present" >}}

```
A web ACL defines a collection of rules to use to inspect and control web requests. Each rule has an action defined
(allow, block, or count) for requests that match the statement of the rule. In the web ACL, you assign a default
action to take (allow, block) for any request that does not match any of the rules. The rules in a web ACL can be
a combination of the types Rule , RuleGroup , and managed rule group. You can associate a web ACL with one or more
Amazon Web Services resources to protect. The resources can be an Amazon CloudFront distribution, an Amazon API
Gateway REST API, an Application Load Balancer, or an AppSync GraphQL API.

Args:
    name(text): The name of the web ACL. You cannot change the name of a web ACL after you create it.
    scope(text): Specifies whether this is for an Amazon CloudFront distribution or for a regional application.
        A regional application can be an Application Load Balancer (ALB), an Amazon API Gateway REST API,
        or an AppSync GraphQL API.
        To work with CloudFront, you must also specify the Region US East (N. Virginia) as follows:
          * CLI -- Specify the Region when you use the CloudFront scope: --scope=CLOUDFRONT --region=us-east-1 .
          * API and SDKs -- For all calls, use the Region endpoint us-east-1.
    default_action(Dict[str, Any]): The action to perform if none of the Rules contained in the WebACL match.
        * Block (Dict[str, Any], optional): Specifies that WAF should block requests by default.
            * CustomResponse (Dict[str, Any], optional): Defines a custom response for the web request. For information about customizing web requests
                and responses, see Customizing web requests and responses in WAF in the WAF Developer Guide.
                * ResponseCode (int): The HTTP status code to return to the client.  For a list of status codes that you can use in
                    your custom reqponses, see Supported status codes for custom response in the WAF Developer
                    Guide.
                * CustomResponseBodyKey (str, optional): References the response body that you want WAF to return to the web request client. You can
                    define a custom response for a rule action or a default web ACL action that is set to block. To
                    do this, you first define the response body key and value in the CustomResponseBodies setting
                    for the WebACL or RuleGroup where you want to use it. Then, in the rule action or web ACL
                    default action BlockAction setting, you reference the response body using this key.
                * ResponseHeaders (List[Dict[str, Any]], optional): The HTTP headers to use in the response. Duplicate header names are not allowed.  For
                    information about the limits on count and size for custom request and response settings, see WAF
                    quotas in the WAF Developer Guide.
                    * Name (str): The name of the custom header.  For custom request header insertion, when WAF inserts the header
                        into the request, it prefixes this name x-amzn-waf-, to avoid confusion with the headers that
                        are already in the request. For example, for the header name sample, WAF inserts the header
                        x-amzn-waf-sample.
                    * Value (str): The value of the custom header.
        * Allow (Dict[str, Any], optional): Specifies that WAF should allow requests by default.
            * CustomRequestHandling (Dict[str, Any], optional): Defines custom handling for the web request. For information about customizing web requests and
                responses, see Customizing web requests and responses in WAF in the WAF Developer Guide.
                * InsertHeaders (List['CustomHTTPHeader']): The HTTP headers to insert into the request. Duplicate header names are not allowed.  For
                    information about the limits on count and size for custom request and response settings, see WAF
                    quotas in the WAF Developer Guide.
    visibility_config(Dict[str, Any]): Defines and enables Amazon CloudWatch metrics and web request sample collection.
        * SampledRequestsEnabled (bool): A boolean indicating whether WAF should store a sampling of the web requests that match the
            rules. You can view the sampled requests through the WAF console.
        * CloudWatchMetricsEnabled (bool): A boolean indicating whether the associated resource sends metrics to Amazon CloudWatch. For the
            list of available metrics, see WAF Metrics.
        * MetricName (str): A name of the Amazon CloudWatch metric. The name can contain only the characters: A-Z, a-z, 0-9,
            - (hyphen), and _ (underscore). The name can be from one to 128 characters long. It can't
            contain whitespace or metric names reserved for WAF, for example "All" and "Default_Action."
    resource_id(text, optional): AWS WAF ID.
    description(text, optional): A description of the web ACL that helps with identification.
    rules(List[Dict[str, Any]], optional): The Rule statements used to identify the web requests that you want to allow, block, or count.
            Each rule includes one top-level statement that WAF uses to identify matching web requests, and
            parameters that govern how WAF handles them. Defaults to None.
        * Name (str): The name of the rule. You can't change the name of a Rule after you create it.
        * Priority (int): If you define more than one Rule in a WebACL, WAF evaluates each request against the Rules in
            order based on the value of Priority. WAF processes rules with lower priority first. The
            priorities don't need to be consecutive, but they must all be different.
            * Statement (Dict[str, Any]): The WAF processing statement for the rule, for example ByteMatchStatement or
            SizeConstraintStatement.
            * ByteMatchStatement (Dict[str, Any], optional): A rule statement that defines a string match search for WAF to apply to web requests. The byte
                match statement provides the bytes to search for, the location in requests that you want WAF to
                search, and other settings. The bytes to search for are typically a string that corresponds with
                ASCII characters. In the WAF console and the developer guide, this is refered to as a string
                match statement.
                * SearchString (ByteString): A string value that you want WAF to search for.
                * FieldToMatch (Dict[str, Any]): The part of the web request that you want WAF to inspect. For more information, see
                    FieldToMatch.
                    * SingleHeader (Dict[str, Any], optional): Inspect a single header. Provide the name of the header to inspect, for example, User-Agent or
                        Referer. This setting isn't case sensitive. Example JSON: "SingleHeader": { "Name": "haystack" }
                        Alternately, you can filter and inspect all headers with the Headers FieldToMatch setting.
                        * Name (str): The name of the query header to inspect.
                    * SingleQueryArgument (Dict[str, Any], optional): Inspect a single query argument. Provide the name of the query argument to inspect, such as
                        UserName or SalesRegion. The name can be up to 30 characters long and isn't case sensitive.
                        Example JSON: "SingleQueryArgument": { "Name": "myArgument" }
                        * Name (str): The name of the query argument to inspect.
                    * AllQueryArguments (Dict, optional): Inspect all query arguments.
                    * UriPath (Dict, optional): Inspect the request URI path. This is the part of the web request that identifies a resource,
                        for example, /images/daily-ad.jpg.
                    * QueryString (Dict, optional): Inspect the query string. This is the part of a URL that appears after a ? character, if any.
                    * Body (Dict[str, Any], optional): Inspect the request body as plain text. The request body immediately follows the request
                        headers. This is the part of a request that contains any additional data that you want to send
                        to your web server as the HTTP request body, such as data from a form.  Only the first 8 KB
                        (8192 bytes) of the request body are forwarded to WAF for inspection by the underlying host
                        service. For information about how to handle oversized request bodies, see the Body object
                        configuration.
                        * OversizeHandling (str, optional): What WAF should do if the body is larger than WAF can inspect.
                    * Method (Dict, optional): Inspect the HTTP method. The method indicates the type of operation that the request is asking
                        the origin to perform.
                    * JsonBody (Dict[str, Any], optional): Inspect the request body as JSON. The request body immediately follows the request headers. This
                        is the part of a request that contains any additional data that you want to send to your web
                        server as the HTTP request body, such as data from a form.  Only the first 8 KB (8192 bytes) of
                        the request body are forwarded to WAF for inspection by the underlying host service. For
                        information about how to handle oversized request bodies, see the JsonBody object configuration.
                        * MatchPattern (Dict[str, Any]): The patterns to look for in the JSON body. WAF inspects the results of these pattern matches
                            against the rule inspection criteria.
                            * All (Dict, optional): Match all of the elements. See also MatchScope in JsonBody.  You must specify either this
                                setting or the IncludedPaths setting, but not both.
                            * IncludedPaths (List[str], optional): Match only the specified include paths. See also MatchScope in JsonBody.  Provide the include
                                paths using JSON Pointer syntax. For example, "IncludedPaths": ["/dogs/0/name", "/dogs/1/name"].
                                For information about this syntax, see the Internet Engineering Task Force (IETF) documentation
                                JavaScript Object Notation (JSON) Pointer.  You must specify either this setting or the All
                                setting, but not both.  Don't use this option to include all paths. Instead, use the All
                                setting.
                        * MatchScope (str): The parts of the JSON to match against using the MatchPattern. If you specify All, WAF matches
                            against keys and values.
                        * InvalidFallbackBehavior (str, optional): What WAF should do if it fails to completely parse the JSON body.
                            The options are the following:
                                EVALUATE_AS_STRING - Inspect the body as plain text. WAF applies the text transformations and
                                    inspection criteria that you defined for the JSON inspection to the body text string.
                                MATCH - Treat the web request as matching the rule statement. WAF applies the rule action to the request.
                                NO_MATCH - Treat the web request as not matching the rule statement.
                        * OversizeHandling (str, optional): What WAF should do if the body is larger than WAF can inspect.
                    * Headers (Dict[str, Any], optional): Inspect the request headers. You must configure scope and pattern matching filters in the
                        Headers object, to define the set of headers to and the parts of the headers that WAF inspects.
                        Only the first 8 KB (8192 bytes) of a request's headers and only the first 200 headers are
                        forwarded to WAF for inspection by the underlying host service. You must configure how to handle
                        any oversize header content in the Headers object. WAF applies the pattern matching filters to
                        the headers that it receives from the underlying host service.
                        * MatchPattern (Dict[str, Any]): The filter to use to identify the subset of headers to inspect in a web request.  You must
                            specify exactly one setting: either All, IncludedHeaders, or ExcludedHeaders. Example JSON:
                            "HeaderMatchPattern": { "ExcludedHeaders": {"KeyToExclude1", "KeyToExclude2"} }
                            * All (Dict, optional): Inspect all headers.
                            * IncludedHeaders (List[str], optional): Inspect only the headers that have a key that matches one of the strings specified here.
                            * ExcludedHeaders (List[str], optional): Inspect only the headers whose keys don't match any of the strings specified here.
                        * MatchScope (str): The parts of the headers to match with the rule inspection criteria. If you specify All, WAF
                            inspects both keys and values.
                        * OversizeHandling (str): What WAF should do if the headers of the request are larger than WAF can inspect.
                    * Cookies (Dict[str, Any], optional): Inspect the request cookies. You must configure scope and pattern matching filters in the
                        Cookies object, to define the set of cookies and the parts of the cookies that WAF inspects.
                        Only the first 8 KB (8192 bytes) of a request's cookies and only the first 200 cookies are
                        forwarded to WAF for inspection by the underlying host service. You must configure how to handle
                        any oversize cookie content in the Cookies object. WAF applies the pattern matching filters to
                        the cookies that it receives from the underlying host service.
                        * MatchPattern (Dict[str, Any]): The filter to use to identify the subset of cookies to inspect in a web request.  You must
                            specify exactly one setting: either All, IncludedCookies, or ExcludedCookies. Example JSON:
                            "CookieMatchPattern": { "IncludedCookies": {"KeyToInclude1", "KeyToInclude2", "KeyToInclude3"} }
                            * All (Dict, optional): Inspect all cookies.
                            * IncludedCookies (List[str], optional): Inspect only the cookies that have a key that matches one of the strings specified here.
                            * ExcludedCookies (List[str], optional): Inspect only the cookies whose keys don't match any of the strings specified here.
                        * MatchScope (str): The parts of the cookies to inspect with the rule inspection criteria. If you specify All, WAF
                            inspects both keys and values.
                        * OversizeHandling (str): What WAF should do if the cookies of the request are larger than WAF can inspect.
                * TextTransformations (List[Dict[str, Any]]): Text transformations eliminate some of the unusual formatting that attackers use in web requests
                    in an effort to bypass detection. If you specify one or more transformations in a rule
                    statement, WAF performs all transformations on the content of the request component identified
                    by FieldToMatch, starting from the lowest priority setting, before inspecting the content for a
                    match.
                    * Priority (int): Sets the relative processing order for multiple transformations that are defined for a rule
                        statement. WAF processes all transformations, from lowest priority to highest, before inspecting
                        the transformed content. The priorities don't need to be consecutive, but they must all be
                        different.
                    * Type (str): You can specify the following transformation types:
                        BASE64_DECODE - Decode a Base64-encoded string.
                        BASE64_DECODE_EXT - Decode a Base64-encoded string, but use a forgiving implementation
                            that ignores characters that aren't valid.
                        CMD_LINE - Command-line transformations. These are helpful in reducing effectiveness of attackers who inject an operating system command-line
                            command and use unusual formatting to disguise some or all of the command.
                * PositionalConstraint (str): The area within the portion of the web request that you want WAF to search for SearchString.
                    Valid values include the following:  CONTAINS  The specified part of the web request must
                    include the value of SearchString, but the location doesn't matter.  CONTAINS_WORD  The
                    specified part of the web request must include the value of SearchString, and SearchString must
                    contain only alphanumeric characters or underscore (A-Z, a-z, 0-9, or _). In addition,
                    SearchString must be a word, which means that both of the following are true:    SearchString is
                    at the beginning of the specified part of the web request or is preceded by a character other
                    than an alphanumeric character or underscore (_). Examples include the value of a header and
                    ;BadBot.    SearchString is at the end of the specified part of the web request or is followed
                    by a character other than an alphanumeric character or underscore (_), for example, BadBot; and
                    -BadBot;.    EXACTLY  The value of the specified part of the web request must exactly match the
                    value of SearchString.  STARTS_WITH  The value of SearchString must appear at the beginning of
                    the specified part of the web request.  ENDS_WITH  The value of SearchString must appear at the
                    end of the specified part of the web request.
            * SqliMatchStatement (Dict[str, Any], optional): Attackers sometimes insert malicious SQL code into web requests in an effort to extract data
                from your database. To allow or block web requests that appear to contain malicious SQL code,
                create one or more SQL injection match conditions. An SQL injection match condition identifies
                the part of web requests, such as the URI or the query string, that you want WAF to inspect.
                Later in the process, when you create a web ACL, you specify whether to allow or block requests
                that appear to contain malicious SQL code.
                * FieldToMatch ('FieldToMatch'): The part of the web request that you want WAF to inspect. For more information, see
                    FieldToMatch.
                * TextTransformations (List['TextTransformation']): Text transformations eliminate some of the unusual formatting that attackers use in web requests
                    in an effort to bypass detection. If you specify one or more transformations in a rule
                    statement, WAF performs all transformations on the content of the request component identified
                    by FieldToMatch, starting from the lowest priority setting, before inspecting the content for a
                    match.
            * XssMatchStatement (Dict[str, Any], optional): A rule statement that defines a cross-site scripting (XSS) match search for WAF to apply to web
                requests. XSS attacks are those where the attacker uses vulnerabilities in a benign website as a
                vehicle to inject malicious client-site scripts into other legitimate web browsers. The XSS
                match statement provides the location in requests that you want WAF to search and text
                transformations to use on the search area before WAF searches for character sequences that are
                likely to be malicious strings.
                * FieldToMatch ('FieldToMatch'): The part of the web request that you want WAF to inspect. For more information, see
                    FieldToMatch.
                * TextTransformations (List['TextTransformation']): Text transformations eliminate some of the unusual formatting that attackers use in web requests
                    in an effort to bypass detection. If you specify one or more transformations in a rule
                    statement, WAF performs all transformations on the content of the request component identified
                    by FieldToMatch, starting from the lowest priority setting, before inspecting the content for a
                    match.
            * SizeConstraintStatement (Dict[str, Any], optional): A rule statement that compares a number of bytes against the size of a request component, using
                    a comparison operator, such as greater than (>) or less than (<). For example, you can use a
                    size constraint statement to look for query strings that are longer than 100 bytes.  If you
                    configure WAF to inspect the request body, WAF inspects only the first 8192 bytes (8 KB). If the
                    request body for your web requests never exceeds 8192 bytes, you can create a size constraint
                    condition and block requests that have a request body greater than 8192 bytes. If you choose URI
                    for the value of Part of the request to filter on, the slash (/) in the URI counts as one
                    character. For example, the URI /logo.jpg is nine characters long.
                * FieldToMatch ('FieldToMatch'): The part of the web request that you want WAF to inspect. For more information, see
                    FieldToMatch.
                * ComparisonOperator (str): The operator to use to compare the request part to the size setting.
                * Size (int): The size, in byte, to compare to the request part, after any transformations.
                * TextTransformations (List['TextTransformation']): Text transformations eliminate some of the unusual formatting that attackers use in web requests
                    in an effort to bypass detection. If you specify one or more transformations in a rule
                    statement, WAF performs all transformations on the content of the request component identified
                    by FieldToMatch, starting from the lowest priority setting, before inspecting the content for a
                    match.
            * GeoMatchStatement (Dict[str, Any], optional): A rule statement used to identify web requests based on country of origin.
                * CountryCodes (List[str], optional): An array of two-character country codes, for example, [ "US", "CN" ], from the alpha-2 country
                    ISO codes of the ISO 3166 international standard.
                * ForwardedIPConfig (Dict[str, Any], optional): The configuration for inspecting IP addresses in an HTTP header that you specify, instead of
                    using the IP address that's reported by the web request origin. Commonly, this is the
                    X-Forwarded-For (XFF) header, but you can specify any header name.   If the specified header
                    isn't present in the request, WAF doesn't apply the rule to the web request at all.
                    * HeaderName (str): The name of the HTTP header to use for the IP address. For example, to use the X-Forwarded-For
                        (XFF) header, set this to X-Forwarded-For.  If the specified header isn't present in the
                        request, WAF doesn't apply the rule to the web request at all.
                    * FallbackBehavior (str): The match status to assign to the web request if the request doesn't have a valid IP address in
                        the specified position.  If the specified header isn't present in the request, WAF doesn't apply
                        the rule to the web request at all.  You can specify the following fallback behaviors:
                            MATCH - Treat the web request as matching the rule statement. WAF applies the rule action to the request.
                            NO_MATCH - Treat the web request as not matching the rule statement.
            * RuleGroupReferenceStatement (Dict[str, Any], optional): A rule statement used to run the rules that are defined in a RuleGroup. To use this, create a
                rule group with your rules, then provide the ARN of the rule group in this statement. You cannot
                nest a RuleGroupReferenceStatement, for example for use inside a NotStatement or OrStatement.
                You can only use a rule group reference statement at the top level inside a web ACL.
                * ARN (str): The Amazon Resource Name (ARN) of the entity.
                * ExcludedRules (List[Dict[str, Any]], optional): The rules in the referenced rule group whose actions are set to Count. When you exclude a rule,
                    WAF evaluates it exactly as it would if the rule action setting were Count. This is a useful
                    option for testing the rules in a rule group without modifying how they handle your web traffic.
                    * Name (str): The name of the rule whose action you want to override to Count.
            * IPSetReferenceStatement (Dict[str, Any], optional): A rule statement used to detect web requests coming from particular IP addresses or address
                ranges. To use this, create an IPSet that specifies the addresses you want to detect, then use
                the ARN of that set in this statement. To create an IP set, see CreateIPSet. Each IP set rule
                statement references an IP set. You create and maintain the set independent of your rules. This
                allows you to use the single set in multiple rules. When you update the referenced set, WAF
                automatically updates all rules that reference it.
                * ARN (str): The Amazon Resource Name (ARN) of the IPSet that this statement references.
                * IPSetForwardedIPConfig (Dict[str, Any], optional): The configuration for inspecting IP addresses in an HTTP header that you specify, instead of
                    using the IP address that's reported by the web request origin. Commonly, this is the
                    X-Forwarded-For (XFF) header, but you can specify any header name.   If the specified header
                    isn't present in the request, WAF doesn't apply the rule to the web request at all.
                    * HeaderName (str): The name of the HTTP header to use for the IP address. For example, to use the X-Forwarded-For
                        (XFF) header, set this to X-Forwarded-For.  If the specified header isn't present in the
                        request, WAF doesn't apply the rule to the web request at all.
                    * FallbackBehavior (str): The match status to assign to the web request if the request doesn't have a valid IP address in
                        the specified position.  If the specified header isn't present in the request, WAF doesn't apply
                        the rule to the web request at all.  You can specify the following fallback behaviors:
                            MATCH - Treat the web request as matching the rule statement. WAF applies the rule action to the request.
                            NO_MATCH - Treat the web request as not matching the rule statement.
                    * Position (str): The position in the header to search for the IP address. The header can contain IP addresses of
                        the original client and also of proxies. For example, the header value could be 10.1.1.1,
                        127.0.0.0, 10.10.10.10 where the first IP address identifies the original client and the rest
                        identify proxies that the request went through.  The options for this setting are the following:
                        FIRST - Inspect the first IP address in the list of IP addresses in the header. This is usually
                        the client's original IP.   LAST - Inspect the last IP address in the list of IP addresses in
                        the header.   ANY - Inspect all IP addresses in the header for a match. If the header contains
                        more than 10 IP addresses, WAF inspects the last 10.
            * RegexPatternSetReferenceStatement (Dict[str, Any], optional): A rule statement used to search web request components for matches with regular expressions. To
                use this, create a RegexPatternSet that specifies the expressions that you want to detect, then
                use the ARN of that set in this statement. A web request matches the pattern set rule statement
                if the request component matches any of the patterns in the set. To create a regex pattern set,
                see CreateRegexPatternSet. Each regex pattern set rule statement references a regex pattern set.
                You create and maintain the set independent of your rules. This allows you to use the single set
                in multiple rules. When you update the referenced set, WAF automatically updates all rules that
                reference it.
                * ARN (str): The Amazon Resource Name (ARN) of the RegexPatternSet that this statement references.
                * FieldToMatch ('FieldToMatch'): The part of the web request that you want WAF to inspect. For more information, see
                    FieldToMatch.
                * TextTransformations (List['TextTransformation']): Text transformations eliminate some of the unusual formatting that attackers use in web requests
                    in an effort to bypass detection. If you specify one or more transformations in a rule
                    statement, WAF performs all transformations on the content of the request component identified
                    by FieldToMatch, starting from the lowest priority setting, before inspecting the content for a
                    match.
            * RateBasedStatement (Dict[str, Any], optional): A rate-based rule tracks the rate of requests for each originating IP address, and triggers the
                rule action when the rate exceeds a limit that you specify on the number of requests in any
                5-minute time span. You can use this to put a temporary block on requests from an IP address
                that is sending excessive requests.  WAF tracks and manages web requests separately for each
                instance of a rate-based rule that you use. For example, if you provide the same rate-based rule
                settings in two web ACLs, each of the two rule statements represents a separate instance of the
                rate-based rule and gets its own tracking and management by WAF. If you define a rate-based rule
                inside a rule group, and then use that rule group in multiple places, each use creates a
                separate instance of the rate-based rule that gets its own tracking and management by WAF.  When
                the rule action triggers, WAF blocks additional requests from the IP address until the request
                rate falls below the limit. You can optionally nest another statement inside the rate-based
                statement, to narrow the scope of the rule so that it only counts requests that match the nested
                statement. For example, based on recent requests that you have seen from an attacker, you might
                create a rate-based rule with a nested AND rule statement that contains the following nested
                statements:   An IP match statement with an IP set that specified the address 192.0.2.44.   A
                string match statement that searches in the User-Agent header for the string BadBot.   In this
                rate-based rule, you also define a rate limit. For this example, the rate limit is 1,000.
                Requests that meet both of the conditions in the statements are counted. If the count exceeds
                1,000 requests per five minutes, the rule action triggers. Requests that do not meet both
                conditions are not counted towards the rate limit and are not affected by this rule. You cannot
                nest a RateBasedStatement inside another statement, for example inside a NotStatement or
                OrStatement. You can define a RateBasedStatement inside a web ACL and inside a rule group.
                * Limit (int): The limit on requests per 5-minute period for a single originating IP address. If the statement
                    includes a ScopeDownStatement, this limit is applied only to the requests that match the
                    statement.
                * AggregateKeyType (str): Setting that indicates how to aggregate the request counts. The options are the following:
                   IP - Aggregate the request counts on the IP address from the web request origin.
                   FORWARDED_IP - Aggregate the request counts on the first IP address in an HTTP header. If you use this,
                    configure the ForwardedIPConfig, to specify the header to use.
                * ScopeDownStatement ('Statement', optional): An optional nested statement that narrows the scope of the web requests that are evaluated by
                    the rate-based statement. Requests are only tracked by the rate-based statement if they match
                    the scope-down statement. You can use any nestable Statement in the scope-down statement, and
                    you can nest statements at any level, the same as you can for a rule statement.
                * ForwardedIPConfig ('ForwardedIPConfig', optional): The configuration for inspecting IP addresses in an HTTP header that you specify, instead of
                    using the IP address that's reported by the web request origin. Commonly, this is the
                    X-Forwarded-For (XFF) header, but you can specify any header name.   If the specified header
                    isn't present in the request, WAF doesn't apply the rule to the web request at all.  This is
                    required if AggregateKeyType is set to FORWARDED_IP.
            * AndStatement (Dict[str, Any], optional): A logical rule statement used to combine other rule statements with AND logic. You provide more
                than one Statement within the AndStatement.
                * Statements (List[Dict[str, Any]]): The statements to combine with AND logic. You can use any statements that can be nested.
                    * ByteMatchStatement ('ByteMatchStatement', optional): A rule statement that defines a string match search for WAF to apply to web requests. The byte
                        match statement provides the bytes to search for, the location in requests that you want WAF to
                        search, and other settings. The bytes to search for are typically a string that corresponds with
                        ASCII characters. In the WAF console and the developer guide, this is refered to as a string
                        match statement.
                    * SqliMatchStatement ('SqliMatchStatement', optional): Attackers sometimes insert malicious SQL code into web requests in an effort to extract data
                        from your database. To allow or block web requests that appear to contain malicious SQL code,
                        create one or more SQL injection match conditions. An SQL injection match condition identifies
                        the part of web requests, such as the URI or the query string, that you want WAF to inspect.
                        Later in the process, when you create a web ACL, you specify whether to allow or block requests
                        that appear to contain malicious SQL code.
                    * XssMatchStatement ('XssMatchStatement', optional): A rule statement that defines a cross-site scripting (XSS) match search for WAF to apply to web
                        requests. XSS attacks are those where the attacker uses vulnerabilities in a benign website as a
                        vehicle to inject malicious client-site scripts into other legitimate web browsers. The XSS
                        match statement provides the location in requests that you want WAF to search and text
                        transformations to use on the search area before WAF searches for character sequences that are
                        likely to be malicious strings.
                    * SizeConstraintStatement ('SizeConstraintStatement', optional): A rule statement that compares a number of bytes against the size of a request component, using
                        a comparison operator, such as greater than (>) or less than (<). For example, you can use a
                        size constraint statement to look for query strings that are longer than 100 bytes.  If you
                        configure WAF to inspect the request body, WAF inspects only the first 8192 bytes (8 KB). If the
                        request body for your web requests never exceeds 8192 bytes, you can create a size constraint
                        condition and block requests that have a request body greater than 8192 bytes. If you choose URI
                        for the value of Part of the request to filter on, the slash (/) in the URI counts as one
                        character. For example, the URI /logo.jpg is nine characters long.
                    * GeoMatchStatement ('GeoMatchStatement', optional): A rule statement used to identify web requests based on country of origin.
                    * RuleGroupReferenceStatement ('RuleGroupReferenceStatement', optional): A rule statement used to run the rules that are defined in a RuleGroup. To use this, create a
                        rule group with your rules, then provide the ARN of the rule group in this statement. You cannot
                        nest a RuleGroupReferenceStatement, for example for use inside a NotStatement or OrStatement.
                        You can only use a rule group reference statement at the top level inside a web ACL.
                    * IPSetReferenceStatement ('IPSetReferenceStatement', optional): A rule statement used to detect web requests coming from particular IP addresses or address
                        ranges. To use this, create an IPSet that specifies the addresses you want to detect, then use
                        the ARN of that set in this statement. To create an IP set, see CreateIPSet. Each IP set rule
                        statement references an IP set. You create and maintain the set independent of your rules. This
                        allows you to use the single set in multiple rules. When you update the referenced set, WAF
                        automatically updates all rules that reference it.
                    * RegexPatternSetReferenceStatement ('RegexPatternSetReferenceStatement', optional): A rule statement used to search web request components for matches with regular expressions. To
                        use this, create a RegexPatternSet that specifies the expressions that you want to detect, then
                        use the ARN of that set in this statement. A web request matches the pattern set rule statement
                        if the request component matches any of the patterns in the set. To create a regex pattern set,
                        see CreateRegexPatternSet. Each regex pattern set rule statement references a regex pattern set.
                        You create and maintain the set independent of your rules. This allows you to use the single set
                        in multiple rules. When you update the referenced set, WAF automatically updates all rules that
                        reference it.
                    * RateBasedStatement ('RateBasedStatement', optional): A rate-based rule tracks the rate of requests for each originating IP address, and triggers the
                        rule action when the rate exceeds a limit that you specify on the number of requests in any
                        5-minute time span. You can use this to put a temporary block on requests from an IP address
                        that is sending excessive requests.  WAF tracks and manages web requests separately for each
                        instance of a rate-based rule that you use. For example, if you provide the same rate-based rule
                        settings in two web ACLs, each of the two rule statements represents a separate instance of the
                        rate-based rule and gets its own tracking and management by WAF. If you define a rate-based rule
                        inside a rule group, and then use that rule group in multiple places, each use creates a
                        separate instance of the rate-based rule that gets its own tracking and management by WAF.  When
                        the rule action triggers, WAF blocks additional requests from the IP address until the request
                        rate falls below the limit. You can optionally nest another statement inside the rate-based
                        statement, to narrow the scope of the rule so that it only counts requests that match the nested
                        statement. For example, based on recent requests that you have seen from an attacker, you might
                        create a rate-based rule with a nested AND rule statement that contains the following nested
                        statements:   An IP match statement with an IP set that specified the address 192.0.2.44.   A
                        string match statement that searches in the User-Agent header for the string BadBot.   In this
                        rate-based rule, you also define a rate limit. For this example, the rate limit is 1,000.
                        Requests that meet both of the conditions in the statements are counted. If the count exceeds
                        1,000 requests per five minutes, the rule action triggers. Requests that do not meet both
                        conditions are not counted towards the rate limit and are not affected by this rule. You cannot
                        nest a RateBasedStatement inside another statement, for example inside a NotStatement or
                        OrStatement. You can define a RateBasedStatement inside a web ACL and inside a rule group.
                    * AndStatement ('AndStatement', optional): A logical rule statement used to combine other rule statements with AND logic. You provide more
                        than one Statement within the AndStatement.
                    * OrStatement (Dict[str, Any], optional): A logical rule statement used to combine other rule statements with OR logic. You provide more
                        than one Statement within the OrStatement.
                        * Statements (List['Statement']): The statements to combine with OR logic. You can use any statements that can be nested.
                    * NotStatement (Dict[str, Any], optional): A logical rule statement used to negate the results of another rule statement. You provide one
                        Statement within the NotStatement.
                        * Statement ('Statement'): The statement to negate. You can use any statement that can be nested.
                    * ManagedRuleGroupStatement (Dict[str, Any], optional): A rule statement used to run the rules that are defined in a managed rule group. To use this,
                        provide the vendor name and the name of the rule group in this statement. You can retrieve the
                        required names by calling ListAvailableManagedRuleGroups. You cannot nest a
                        ManagedRuleGroupStatement, for example for use inside a NotStatement or OrStatement. It can only
                        be referenced as a top-level statement within a rule.
                        * VendorName (str): The name of the managed rule group vendor. You use this, along with the rule group name, to
                            identify the rule group.
                        * Name (str): The name of the managed rule group. You use this, along with the vendor name, to identify the
                            rule group.
                        * Version (str, optional): The version of the managed rule group to use. If you specify this, the version setting is fixed
                            until you change it. If you don't specify this, WAF uses the vendor's default version, and then
                            keeps the version at the vendor's default when the vendor updates the managed rule group
                            settings.
                        * ExcludedRules (List['ExcludedRule'], optional): The rules in the referenced rule group whose actions are set to Count. When you exclude a rule,
                            WAF evaluates it exactly as it would if the rule action setting were Count. This is a useful
                            option for testing the rules in a rule group without modifying how they handle your web traffic.
                        * ScopeDownStatement ('Statement', optional): An optional nested statement that narrows the scope of the web requests that are evaluated by
                            the managed rule group. Requests are only evaluated by the rule group if they match the scope-
                            down statement. You can use any nestable Statement in the scope-down statement, and you can nest
                            statements at any level, the same as you can for a rule statement.
                        * ManagedRuleGroupConfigs (List[Dict[str, Any]], optional): Additional information that's used by a managed rule group. Most managed rule groups don't
                            require this. Use this for the account takeover prevention managed rule group
                            AWSManagedRulesATPRuleSet, to provide information about the sign-in page of your application.
                            You can provide multiple individual ManagedRuleGroupConfig objects for any rule group
                            configuration, for example UsernameField and PasswordField. The configuration that you provide
                            depends on the needs of the managed rule group. For the ATP managed rule group, you provide the
                            following individual configuration objects: LoginPath, PasswordField, PayloadType and
                            UsernameField.
                            * LoginPath (str, optional): The path of the login endpoint for your application. For example, for the URL
                                https://example.com/web/login, you would provide the path /web/login.
                            * PayloadType (str, optional): The payload type for your login endpoint, either JSON or form encoded.
                            * UsernameField (Dict[str, Any], optional): Details about your login page username field.
                                * Identifier (str): The name of the username field. For example /form/username.
                            * PasswordField (Dict[str, Any], optional): Details about your login page password field.
                                * Identifier (str): The name of the password field. For example /form/password.
                    * LabelMatchStatement (Dict[str, Any], optional): A rule statement that defines a string match search against labels that have been added to the
                        web request by rules that have already run in the web ACL.  The label match statement provides
                        the label or namespace string to search for. The label string can represent a part or all of the
                        fully qualified label name that had been added to the web request. Fully qualified labels have a
                        prefix, optional namespaces, and label name. The prefix identifies the rule group or web ACL
                        context of the rule that added the label. If you do not provide the fully qualified name in your
                        label match string, WAF performs the search for labels that were added in the same context as
                        the label match statement.
                        * Scope (str): Specify whether you want to match using the label name or just the namespace.
                        * Key (str): The string to match against. The setting you provide for this depends on the match statement's
                            Scope setting:    If the Scope indicates LABEL, then this specification must include the name
                            and can include any number of preceding namespace specifications and prefix up to providing the
                            fully qualified label name.    If the Scope indicates NAMESPACE, then this specification can
                            include any number of contiguous namespace strings, and can include the entire label namespace
                            prefix from the rule group or web ACL where the label originates.   Labels are case sensitive
                            and components of a label must be separated by colon, for example NS1:NS2:name.
                    * RegexMatchStatement (Dict[str, Any], optional): A rule statement used to search web request components for a match against a single regular
                        expression.
                        * RegexString (str): The string representing the regular expression.
                        * FieldToMatch ('FieldToMatch'): The part of the web request that you want WAF to inspect. For more information, see
                            FieldToMatch.
                        * TextTransformations (List['TextTransformation']): Text transformations eliminate some of the unusual formatting that attackers use in web requests
                            in an effort to bypass detection. If you specify one or more transformations in a rule
                            statement, WAF performs all transformations on the content of the request component identified
                            by FieldToMatch, starting from the lowest priority setting, before inspecting the content for a
                            match.
            * OrStatement ('OrStatement', optional): A logical rule statement used to combine other rule statements with OR logic. You provide more
                than one Statement within the OrStatement.
            * NotStatement ('NotStatement', optional): A logical rule statement used to negate the results of another rule statement. You provide one
                Statement within the NotStatement.
            * ManagedRuleGroupStatement ('ManagedRuleGroupStatement', optional): A rule statement used to run the rules that are defined in a managed rule group. To use this,
                provide the vendor name and the name of the rule group in this statement. You can retrieve the
                required names by calling ListAvailableManagedRuleGroups. You cannot nest a
                ManagedRuleGroupStatement, for example for use inside a NotStatement or OrStatement. It can only
                be referenced as a top-level statement within a rule.
            * LabelMatchStatement ('LabelMatchStatement', optional): A rule statement that defines a string match search against labels that have been added to the
                web request by rules that have already run in the web ACL.  The label match statement provides
                the label or namespace string to search for. The label string can represent a part or all of the
                fully qualified label name that had been added to the web request. Fully qualified labels have a
                prefix, optional namespaces, and label name. The prefix identifies the rule group or web ACL
                context of the rule that added the label. If you do not provide the fully qualified name in your
                label match string, WAF performs the search for labels that were added in the same context as
                the label match statement.
            * RegexMatchStatement ('RegexMatchStatement', optional): A rule statement used to search web request components for a match against a single regular
                expression.
        * Action (Dict[str, Any], optional): The action that WAF should take on a web request when it matches the rule statement. Settings at
            the web ACL level can override the rule action setting.  This is used only for rules whose
            statements do not reference a rule group. Rule statements that reference a rule group include
            RuleGroupReferenceStatement and ManagedRuleGroupStatement.  You must specify either this Action
            setting or the rule OverrideAction setting, but not both:   If the rule statement does not
            reference a rule group, use this rule action setting and not the rule override action setting.
            If the rule statement references a rule group, use the override action setting and not this
            action setting.
            * Block (Dict[str, Any], optional): Instructs WAF to block the web request.
                * CustomResponse (Dict[str, Any], optional): Defines a custom response for the web request. For information about customizing web requests
                    and responses, see Customizing web requests and responses in WAF in the WAF Developer Guide.
                    * ResponseCode (int): The HTTP status code to return to the client.  For a list of status codes that you can use in
                        your custom reqponses, see Supported status codes for custom response in the WAF Developer
                        Guide.
                    * CustomResponseBodyKey (str, optional): References the response body that you want WAF to return to the web request client. You can
                        define a custom response for a rule action or a default web ACL action that is set to block. To
                        do this, you first define the response body key and value in the CustomResponseBodies setting
                        for the WebACL or RuleGroup where you want to use it. Then, in the rule action or web ACL
                        default action BlockAction setting, you reference the response body using this key.
                    * ResponseHeaders (List[Dict[str, Any]], optional): The HTTP headers to use in the response. Duplicate header names are not allowed.  For
                        information about the limits on count and size for custom request and response settings, see WAF
                        quotas in the WAF Developer Guide.
                        * Name (str): The name of the custom header.  For custom request header insertion, when WAF inserts the header
                            into the request, it prefixes this name x-amzn-waf-, to avoid confusion with the headers that
                            are already in the request. For example, for the header name sample, WAF inserts the header
                            x-amzn-waf-sample.
                        * Value (str): The value of the custom header.
            * Allow (Dict[str, Any], optional): Instructs WAF to allow the web request.
                * CustomRequestHandling (Dict[str, Any], optional): Defines custom handling for the web request. For information about customizing web requests and
                    responses, see Customizing web requests and responses in WAF in the WAF Developer Guide.
                    * InsertHeaders (List['CustomHTTPHeader']): The HTTP headers to insert into the request. Duplicate header names are not allowed.  For
                        information about the limits on count and size for custom request and response settings, see WAF
                        quotas in the WAF Developer Guide.
            * Count (Dict[str, Any], optional): Instructs WAF to count the web request and allow it.
                * CustomRequestHandling ('CustomRequestHandling', optional): Defines custom handling for the web request. For information about customizing web requests and
                    responses, see Customizing web requests and responses in WAF in the WAF Developer Guide.
            * Captcha (Dict[str, Any], optional): Instructs WAF to run a CAPTCHA check against the web request.
                * CustomRequestHandling ('CustomRequestHandling', optional): Defines custom handling for the web request. For information about customizing web requests and
                    responses, see Customizing web requests and responses in WAF in the WAF Developer Guide.
        * OverrideAction (Dict[str, Any], optional): The action to use in the place of the action that results from the rule group evaluation. Set
            the override action to none to leave the result of the rule group alone. Set it to count to
            override the result to count only.  You can only use this for rule statements that reference a
            rule group, like RuleGroupReferenceStatement and ManagedRuleGroupStatement.   This option is
            usually set to none. It does not affect how the rules in the rule group are evaluated. If you
            want the rules in the rule group to only count matches, do not use this and instead exclude
            those rules in your rule group reference statement settings.
            * Count ('CountAction', optional): Override the rule group evaluation result to count only.   This option is usually set to none.
                It does not affect how the rules in the rule group are evaluated. If you want the rules in the
                rule group to only count matches, do not use this and instead exclude those rules in your rule
                group reference statement settings.
            * None (Dict, optional): Don't override the rule group evaluation result. This is the most common setting.
        * RuleLabels (List[Dict[str, Any]], optional): Labels to apply to web requests that match the rule match statement. WAF applies fully qualified
            labels to matching web requests. A fully qualified label is the concatenation of a label
            namespace and a rule label. The rule's rule group or web ACL defines the label namespace.  Rules
            that run after this rule in the web ACL can match against these labels using a
            LabelMatchStatement. For each label, provide a case-sensitive string containing optional
            namespaces and a label name, according to the following guidelines:   Separate each component of
            the label with a colon.    Each namespace or name can have up to 128 characters.   You can
            specify up to 5 namespaces in a label.   Don't use the following reserved words in your label
            specification: aws, waf, managed, rulegroup, webacl, regexpatternset, or ipset.   For example,
            myLabelName or nameSpace1:nameSpace2:myLabelName.
            * Name (str): The label string.
        * VisibilityConfig (Dict[str, Any]): Defines and enables Amazon CloudWatch metrics and web request sample collection.
            * SampledRequestsEnabled (bool): A boolean indicating whether WAF should store a sampling of the web requests that match the
                rules. You can view the sampled requests through the WAF console.
            * CloudWatchMetricsEnabled (bool): A boolean indicating whether the associated resource sends metrics to Amazon CloudWatch. For the
                list of available metrics, see WAF Metrics.
            * MetricName (str): A name of the Amazon CloudWatch metric. The name can contain only the characters: A-Z, a-z, 0-9,
                - (hyphen), and _ (underscore). The name can be from one to 128 characters long. It can't
                contain whitespace or metric names reserved for WAF, for example "All" and "Default_Action."
        * CaptchaConfig (Dict[str, Any], optional): Specifies how WAF should handle CAPTCHA evaluations. If you don't specify this, WAF uses the
            CAPTCHA configuration that's defined for the web ACL.
            * ImmunityTimeProperty (Dict[str, Any], optional): Determines how long a CAPTCHA token remains valid after the client successfully solves a CAPTCHA
                puzzle.
                * ImmunityTime (int): The amount of time, in seconds, that a CAPTCHA token is valid. The default setting is 300.
    custom_response_bodies(dict, optional): A map of custom response keys and content bodies. When you create a rule with a
        block action, you can send a custom response to the web request. You define these for the web ACL, and then
        use them in the rules and default actions that you define in the web ACL.
    captcha_config(dict, optional): Specifies how WAF should handle CAPTCHA evaluations for rules that don't have their own
        CaptchaConfig settings. If you don't specify this, WAF uses its default settings for CaptchaConfig.
          * ImmunityTimeProperty (dict) -- Determines how long a CAPTCHA token remains valid after the client
                successfully solves a CAPTCHA puzzle.
              * ImmunityTime(integer) -- The amount of time, in seconds, that a CAPTCHA token is valid. The default
                    setting is 300.
    tags(list, optional): A tag associated with an Amazon Web Services resource. Tags are key:value pairs that you can use to
        categorize and manage your resources, for purposes like billing or other management. Typically, the tag key
        represents a category, such as "environment", and the tag value represents a specific value within that
        category, such as "test," "development," or "production". Or you might set the tag key to "customer" and
        the value to the customer name or ID. You can specify one or more tags to add to each Amazon Web Services
        resource, up to 50 tags for a resource.
        list of tags in the format of [{"Key": tag-key, "Value": tag-value}] or dict in the format of
            {tag-key: tag-value}

Request Syntax:
    [web-acl-name]::
        aws.wafv2.web_acl.present:
        - name: 'string'
        - scope: 'string'
        - default_action: 'dict'
        - description: 'string'
        - rules: ['string']
        - visibility_config: 'dict'
        - custom_response_bodies: 'dict'
        - captcha_config: 'dict'
        - tags:
          - Key: 'string'
            Value: 'string'

Examples:

    .. code-block:: sls
    demo_waf:
        aws.wafv2.web_acl.present:
        - name: demo_waf.
        - scope: REGIONAL
        - default_action:
            Allow: {}
        - description: waf to support REGIONAL resources.
        - rules:
            - Name: AWS-AWSManagedRulesBotControlRuleSet
              OverrideAction:
              None: {}
              Priority: 1
              Statement:
                ManagedRuleGroupStatement:
                Name: AWSManagedRulesBotControlRuleSet
                VendorName: AWS
              VisibilityConfig:
                CloudWatchMetricsEnabled: false
                MetricName: AWS-AWSManagedRulesBotControlRuleSet
                SampledRequestsEnabled: true
        - visibility_config:
            CloudWatchMetricsEnabled: false
            MetricName: test_metric_waf
            SampledRequestsEnabled: true
        - tags:
          - Key: type
            Value: REGIONAL

Returns:
    Dict[str, Any]
```
{{< /tab >}}

{{< /tabs >}}


Full plugin documentation is available on the Idem documentation site - [aws.wafv2.web_acl](https://docs.idemproject.io/idem-aws/en/latest/ref/states/wafv2/web_acl.html).
