# Skip X-Frame-Options for certain URLs in .NET

This example shows rewrite rules that do not apply X-Frame-Options headers to certain URLs. This is helpful when your embedding an iframe into another website that you trust.

    <rewrite>
        <outboundRules>
            <rule name="Add RESPONSE_X-Frame-Options" preCondition="X-Frame-Option not present">
                <match serverVariable="RESPONSE_X_Frame_Options" pattern=".*" />
                <action type="Rewrite" value="DENY" />
                <conditions>
                    <add input="https://something.domain.com/" pattern="https://something.domain.com/" negate="true" />
                </conditions>
            </rule>
            <preConditions>
                <preCondition name="X-Frame-Option not present">
                <add input="{RESPONSE_X_Frame_Options}
                " pattern=".+" negate="true" />
                </preCondition>
            </preConditions>
        </outboundRules>
    </rewrite>
