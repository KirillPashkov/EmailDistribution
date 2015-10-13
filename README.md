Imagine, you have a csv list with several columns where non of them have the correct values, say, for the email adress, but you do know AD has them. (Yes, those things happens a lot!)

You then would like to announce something important to those persons via email with different text messages related to exaclty to certain person.

EmailDistribution script works based on CSV file as input, with AD user lookup to match their attributes and then distribute bulk email with predefined text patterns.

You can load XML configuration file for predefined values if you like. 
Tags and AD filters can be extended via additional records.

XML file example:
```xml
<EmailDistribution Name="Email Distribution" Description="Email Distribution Utility">
    <Configuration Configuration="Configuration Units">
        <Email>
            <SmtpServer>smtpsrv.local</SmtpServer>
            <FromAdress>PashkovKM@RSHB.ru</FromAdress>
            <DisplayName>Pashkov Kirill</DisplayName>   
            <Subject>Weekly Announce</Subject>
            <Priority>Normal</Priority>         
            <!--Recepients for copy/hidden copy. Use ',' as separator for multiplue values-->
            <Cc></Cc>
            <Bcc>PashkovKM@RSHB.ru</Bcc>
        </Email>
        <ADFilter ADFilter="AD search patterns for user accounts lookup">
            <Filter>DisplayName</Filter>
            <Filter>DistinguishedName</Filter>
            <Filter>SamAccountName</Filter>
            <Filter>SID</Filter>
            <Filter>mail</Filter>
            <Filter>EmailAddress</Filter>
        </ADFilter>
        <PatternTag PatternTag="Tag patterns for text transformation">
            <Tag>{FALSE}</Tag>
            <Tag>{PERSON}</Tag>
            <Tag>{ADRESS}</Tag>
            <Tag>{EMAIL}</Tag>
            <Tag>{ID}</Tag>
            <Tag>{SUBJECT}</Tag>
            <Tag>{CUSTOM1}</Tag>
        </PatternTag>
        <Log Log="Logs folder path">
            <!--If not set uses default. Default value is C:\Users\%USERNAME%~1\AppData\Local\Temp-->
            <Path></Path>
        </Log>
        <ADLookupSkip ADLookupSkip="Force to skip AD user account lookup">
            <!--Set to "True" to skip AD user account lookup. Default value is "False"-->
            <Enable>False</Enable>
        </ADLookupSkip>
        <TextPatternSkip TextPatternSkip="Force to skip text pattern load">
            <!--Set to "True" to skip pattern load and use edit mode. Default value is "False"-->
            <Enable>False</Enable>  
        </TextPattearnSkip>
        <UpdateServer>
            <Adress>mycomputer</Adress>
        </UpdateServer> 
    </Configuration>
</EmailDistribution>
```

