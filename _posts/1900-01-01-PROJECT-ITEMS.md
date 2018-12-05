



```sql
/*
-------------------------------------------------------------------
--Create By: Jed Brazal
--Created On: 2014-11-18
--Description:  Objects in a project
-------------------------------------------------------------------
--Change# JED001
--Change by: Jed Brazal
--Cahnge On: 2014-12-04
--Description:  Application Package PeopleCode Object Name
-------------------------------------------------------------------
*/
declare @projectName as varchar(50) = 'UPGCUST'

SELECT PROJD.PROJECTNAME ,
       PROJD.LASTUPDDTTM ,
       PROJD.LASTUPDOPRID ,
       CASE
           WHEN PROJ.OBJECTTYPE = '0' THEN 'Record' + (SELECT CASE 
                                                            WHEN REC.RECTYPE  = '0' THEN ' (SQL Table)'
                                                            WHEN REC.RECTYPE  = '1' THEN ' (SQL View)'
                                                            WHEN REC.RECTYPE  = '2' THEN ' (Derived/Work)'
                                                            WHEN REC.RECTYPE  = '3' THEN ' (Sub Record)'
                                                            WHEN REC.RECTYPE  = '5' THEN ' (Dynamic View)'
                                                            WHEN REC.RECTYPE  = '6' THEN ' (Query View)'
                                                            WHEN REC.RECTYPE  = '7' THEN ' (Temporary Table)' END
                                                             FROM PSRECDEFN REC 
                                                       WHERE REC.RECNAME = PROJ.OBJECTVALUE1)
           WHEN PROJ.OBJECTTYPE = '1' THEN 'Index'
           WHEN PROJ.OBJECTTYPE = '2'
                AND PROJ.OBJECTID2 = '102' THEN 'Field Label'
           WHEN PROJ.OBJECTTYPE = '2'
                AND PROJ.OBJECTID2 <> '102' THEN 'Field'
           WHEN PROJ.OBJECTTYPE = '3' THEN '  Format Definition'
           WHEN PROJ.OBJECTTYPE = '4' THEN 'Translate'
           WHEN PROJ.OBJECTTYPE = '5' THEN 'Page'
           WHEN PROJ.OBJECTTYPE = '6' THEN 'Menu'
           WHEN PROJ.OBJECTTYPE = '7' THEN 'Component'
           WHEN PROJ.OBJECTTYPE = '8' THEN 'Record PeopleCode'
           WHEN PROJ.OBJECTTYPE = '9' THEN '  Menu PeopleCode'
           WHEN PROJ.OBJECTTYPE = '10' THEN 'Query'
           WHEN PROJ.OBJECTTYPE = '11' THEN '  Tree Structure'
           WHEN PROJ.OBJECTTYPE = '12' THEN '  Tree'
           WHEN PROJ.OBJECTTYPE = '13' THEN '  Access Group'
           WHEN PROJ.OBJECTTYPE = '14' THEN '  Color'
           WHEN PROJ.OBJECTTYPE = '15' THEN '  Style'
           WHEN PROJ.OBJECTTYPE = '16' THEN '  Not Used'
           WHEN PROJ.OBJECTTYPE = '17' THEN '  Business Process'
           WHEN PROJ.OBJECTTYPE = '18' THEN 'Activity'
           WHEN PROJ.OBJECTTYPE = '19' THEN '  Role'
           WHEN PROJ.OBJECTTYPE = '20' THEN 'Process Definition' + '(' + LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + ')'
           WHEN PROJ.OBJECTTYPE = '21' THEN '  Process Server'
           WHEN PROJ.OBJECTTYPE = '22' THEN 'Process Type Definition'
           WHEN PROJ.OBJECTTYPE = '23' THEN 'Job Definition'
           WHEN PROJ.OBJECTTYPE = '24' THEN '  Process Recurrence'
           WHEN PROJ.OBJECTTYPE = '25' THEN 'Message Catalog Entry'
           WHEN PROJ.OBJECTTYPE = '26' THEN '  Dimension'
           WHEN PROJ.OBJECTTYPE = '27' THEN '  Analysis Model'
           WHEN PROJ.OBJECTTYPE = '28' THEN '  Cube Template'
           WHEN PROJ.OBJECTTYPE = '29' THEN '  Business Interlink'
           WHEN PROJ.OBJECTTYPE = '30' THEN --'SQL Object'
 CASE
     WHEN PROJ.OBJECTVALUE2 = '0' THEN 'SQL Object'
     WHEN PROJ.OBJECTVALUE2 = '1' THEN 'App Engine SQL'
     WHEN PROJ.OBJECTVALUE2 = '2' THEN 'Record View SQL'
     WHEN PROJ.OBJECTVALUE2 = '5' THEN 'Query for DDAUDIT or SYSAUDIT'
     WHEN PROJ.OBJECTVALUE2 = '6' THEN 'App Engine XML SQL'
     ELSE 'SQL'
 END
           WHEN PROJ.OBJECTTYPE = '31' THEN 'File Layout'
           WHEN PROJ.OBJECTTYPE = '32' THEN 'Component Interface'
           WHEN PROJ.OBJECTTYPE = '33' THEN 'Application Engine Program'
           WHEN PROJ.OBJECTTYPE = '34' THEN 'Application Engine Section'
           WHEN PROJ.OBJECTTYPE = '35' THEN 'Message Node'
           WHEN PROJ.OBJECTTYPE = '36' THEN 'Message Channel'
           WHEN PROJ.OBJECTTYPE = '37' THEN 'Message'
           WHEN PROJ.OBJECTTYPE = '39' THEN 'Message PeopleCode'
           WHEN PROJ.OBJECTTYPE = '40' THEN 'Subscription PeopleCode'
           WHEN PROJ.OBJECTTYPE = '42' THEN 'Component Interface PeopleCode'
           WHEN PROJ.OBJECTTYPE = '43' THEN 'Application Engine PeopleCode'
           WHEN PROJ.OBJECTTYPE = '44' THEN 'Page PeopleCode'
           WHEN PROJ.OBJECTTYPE = '45' THEN 'Page Field PeopleCode'
           WHEN PROJ.OBJECTTYPE = '46' THEN 'Component PeopleCode'
           WHEN PROJ.OBJECTTYPE = '47' THEN 'Component Record PeopleCode'
           WHEN PROJ.OBJECTTYPE = '48' THEN 'Component Record Field PeopleCode'
           WHEN PROJ.OBJECTTYPE = '51' THEN 'HTML'
           WHEN PROJ.OBJECTTYPE = '53' THEN 'Permission List'
           WHEN PROJ.OBJECTTYPE = '54' THEN 'Portal Registry Definition'
           WHEN PROJ.OBJECTTYPE = '55'
                AND PROJ.OBJECTVALUE2 = 'C' THEN 'Portal Registry Structure (Content Reference)'
           WHEN PROJ.OBJECTTYPE = '55'
                AND PROJ.OBJECTVALUE2 = 'F' THEN 'Portal Registry Structure (Folder)'
           WHEN PROJ.OBJECTTYPE = '56' THEN 'URL Definitions'
           WHEN PROJ.OBJECTTYPE = '57' THEN 'Application Package'
           WHEN PROJ.OBJECTTYPE = '58' THEN 'Application Package PeopleCode'
           WHEN PROJ.OBJECTTYPE= '59' THEN '  Portal Registry User Homepage'
           WHEN PROJ.OBJECTTYPE= '60' THEN '  Problem Type Definition'
           WHEN PROJ.OBJECTTYPE= '61' THEN '  Data Archival'
           WHEN PROJ.OBJECTTYPE= '62' THEN '  XSLT'
           WHEN PROJ.OBJECTTYPE= '63' THEN '  Portal Registry User Favorite'
           WHEN PROJ.OBJECTTYPE= '64' THEN '  Mobile Page'
           WHEN PROJ.OBJECTTYPE= '65' THEN '  Relationship'
           WHEN PROJ.OBJECTTYPE= '66' THEN '  Component Interface Property PeopleCode'
           WHEN PROJ.OBJECTTYPE= '67' THEN '  Optimization Model'
           WHEN PROJ.OBJECTTYPE= '68' THEN '  File Reference'
           WHEN PROJ.OBJECTTYPE= '69' THEN '  File Reference Type Code'
           WHEN PROJ.OBJECTTYPE= '70' THEN '  Archive Objects'
           WHEN PROJ.OBJECTTYPE= '71' THEN '  Archive Templates'
           WHEN PROJ.OBJECTTYPE= '72' THEN '  Diagnostic Plug-In'
           WHEN PROJ.OBJECTTYPE= '73' THEN '  BAM Model'
           WHEN PROJ.OBJECTTYPE= '74' THEN '  Not Used'
           WHEN PROJ.OBJECTTYPE= '75' THEN '  Java Portlet User Preferences'
           WHEN PROJ.OBJECTTYPE= '76' THEN '  WSRP Remote Producer'
           WHEN PROJ.OBJECTTYPE= '77' THEN '  WSRP Remote Portlet'
           WHEN PROJ.OBJECTTYPE= '78' THEN '  WSRP Cloned Portlet Handle'
           WHEN PROJ.OBJECTTYPE= '79' THEN '  Service Handle'
           WHEN PROJ.OBJECTTYPE= '80' THEN '  Service Operation Handle'
           WHEN PROJ.OBJECTTYPE= '81' THEN '  Operation Handler Handle'
           WHEN PROJ.OBJECTTYPE= '82' THEN '  Service Operation Version Handle'
           WHEN PROJ.OBJECTTYPE= '83' THEN '  Routing Definition Handle'
           WHEN PROJ.OBJECTTYPE= '84' THEN '  Queue Defintion Handle'
           WHEN PROJ.OBJECTTYPE= '85' THEN '  XMLP Template Defn Manager'
           WHEN PROJ.OBJECTTYPE= '86' THEN '  XMLP Report Defn Manager'
           WHEN PROJ.OBJECTTYPE= '87' THEN '  XMLP File Manager'
           WHEN PROJ.OBJECTTYPE= '88' THEN '  XMLP Data Src Manager'
           WHEN PROJ.OBJECTTYPE= '89' THEN '  WSDL Manager'
           WHEN PROJ.OBJECTTYPE= '90' THEN '  Schema Manager'
           WHEN PROJ.OBJECTTYPE= '91' THEN '  Connected Queries Defn Manager'
           WHEN PROJ.OBJECTTYPE= '92' THEN '  Logical Schema'
           WHEN PROJ.OBJECTTYPE= '93' THEN '  XML Schema'
           WHEN PROJ.OBJECTTYPE= '94' THEN '  Relational Schema'
           WHEN PROJ.OBJECTTYPE= '95' THEN '  Dependency Document'
           WHEN PROJ.OBJECTTYPE= '96' THEN '  Document Schema'
           WHEN PROJ.OBJECTTYPE= '97' THEN '  Essbase Cube Dimension Manager'
           WHEN PROJ.OBJECTTYPE= '98' THEN '  Essbase Cube Outline Manager'
           WHEN PROJ.OBJECTTYPE= '99' THEN '  Essbase Cube Connection Manager'
           WHEN PROJ.OBJECTTYPE= '100' THEN '  Essbase Cube Template Manager'
           WHEN PROJ.OBJECTTYPE= '101' THEN '  Delimited Schema'
           WHEN PROJ.OBJECTTYPE= '102' THEN '  Positional Schema'
           WHEN PROJ.OBJECTTYPE= '103' THEN '  Application Data Set Definition Manager'
           WHEN PROJ.OBJECTTYPE= '104' THEN '  Test Framework Manager'
           WHEN PROJ.OBJECTTYPE= '105' THEN '  Test Framework Test Case Manager'
           WHEN PROJ.OBJECTTYPE= '106' THEN '  Application Data Set Binding'
           WHEN PROJ.OBJECTTYPE= '107' THEN '  Feed Definition Manager'
           WHEN PROJ.OBJECTTYPE= '108' THEN '  Feed Category Manager'
           WHEN PROJ.OBJECTTYPE= '109' THEN '  Feed Data Type Manager'
           WHEN PROJ.OBJECTTYPE= '110' THEN '  Json Schema (will not ship till 8.53)'
           WHEN PROJ.OBJECTTYPE= '111' THEN '  Related Content Service Defintion Manager'
           WHEN PROJ.OBJECTTYPE= '112' THEN '  Related Content Service Manager'
           WHEN PROJ.OBJECTTYPE= '113' THEN '  Related Content Service Config Manager'
           WHEN PROJ.OBJECTTYPE= '114' THEN '  Related Content Layout Manager'
           WHEN PROJ.OBJECTTYPE= '115' THEN '  PTSF Search Attribute'
           WHEN PROJ.OBJECTTYPE= '116' THEN '  PTSF Search Definition'
           WHEN PROJ.OBJECTTYPE= '117' THEN '  PTSF Search Category'
           WHEN PROJ.OBJECTTYPE= '118' THEN '  PTSF Search Context'
           WHEN PROJ.OBJECTTYPE= '119' THEN '  Integration Group Manager'
           WHEN PROJ.OBJECTTYPE= '120' THEN '  Html Schema'
           WHEN PROJ.OBJECTTYPE= '121' THEN '  Document Layout Manager'
           WHEN PROJ.OBJECTTYPE= '122' THEN '  Document Template Manager'
           WHEN PROJ.OBJECTTYPE= '123' THEN '  Composite Query Manager'
           WHEN PROJ.OBJECTTYPE= '124' THEN '  Document PeopleCode Manager'
           WHEN PROJ.OBJECTTYPE= '125' THEN '  MAP Admin Manager'
           ELSE 'Unknown ' + cast(PROJ.OBJECTTYPE AS VARCHAR(5))
       END AS OBJECT_TYPE ,
       CASE
           WHEN PROJ.OBJECTTYPE = '2' AND PROJ.OBJECTID2 = '102' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '  (' + LTRIM(RTRIM(PROJ.OBJECTVALUE2)) + ')'
           WHEN PROJ.OBJECTTYPE = '4' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + ' = ' + LTRIM(RTRIM(PROJ.OBJECTVALUE2))
           WHEN PROJ.OBJECTTYPE = '7' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '.' + LTRIM(RTRIM(PROJ.OBJECTVALUE2))
           WHEN PROJ.OBJECTTYPE = '8' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '.' + LTRIM(RTRIM(PROJ.OBJECTVALUE2)) + '  (' + LTRIM(RTRIM(PROJ.OBJECTVALUE3)) + ')'
           WHEN PROJ.OBJECTTYPE = '20' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE2))
           WHEN PROJ.OBJECTTYPE = '25' THEN 'Message Set : ' + LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '  Messaage Nbr : ' + LTRIM(RTRIM(PROJ.OBJECTVALUE2))
           WHEN PROJ.OBJECTTYPE = '34' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '.' + LTRIM(RTRIM(PROJ.OBJECTVALUE2))
           WHEN PROJ.OBJECTTYPE = '42' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE2)) + '(' + LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + ')'
           WHEN PROJ.OBJECTTYPE = '43' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '.' + SUBSTRING(PROJ.OBJECTVALUE2,1,8) + LTRIM(RTRIM(PROJ.OBJECTVALUE3)) + '(' + LTRIM(RTRIM(PROJ.OBJECTVALUE4)) + ')'
           WHEN PROJ.OBJECTTYPE = '44' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '(' + LTRIM(RTRIM(PROJ.OBJECTVALUE2)) + ')'
           WHEN PROJ.OBJECTTYPE = '45' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '.' + LTRIM(RTRIM(PROJ.OBJECTVALUE2)) + '(' + LTRIM(RTRIM(PROJ.OBJECTVALUE3)) + ')'
           WHEN PROJ.OBJECTTYPE = '46' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '.' + LTRIM(RTRIM(PROJ.OBJECTVALUE2)) + '(' + LTRIM(RTRIM(PROJ.OBJECTVALUE3)) + ')'
           WHEN PROJ.OBJECTTYPE = '47' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '.' + LTRIM(RTRIM(PROJ.OBJECTVALUE2)) + ' ' + LTRIM(RTRIM(PROJ.OBJECTVALUE3)) + '(' + LTRIM(RTRIM(PROJ.OBJECTVALUE4)) + ')'
           WHEN PROJ.OBJECTTYPE = '48' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + '.' + LTRIM(RTRIM(PROJ.OBJECTVALUE2)) + ' ' + LTRIM(RTRIM(PROJ.OBJECTVALUE3)) + '.' + LTRIM(RTRIM(SUBSTRING(PROJ.OBJECTVALUE4,1,18))) + '(' + LTRIM(RTRIM(SUBSTRING(PROJ.OBJECTVALUE4,19,11))) + ')'
           WHEN PROJ.OBJECTTYPE = '55' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + ' ' + LTRIM(RTRIM(PROJ.OBJECTVALUE3))
           WHEN PROJ.OBJECTTYPE = '58' THEN LTRIM(RTRIM(PROJ.OBJECTVALUE1)) + ':' + LTRIM(RTRIM(PROJ.OBJECTVALUE2)) + ':' + LTRIM(RTRIM(PROJ.OBJECTVALUE3)) --JED001 App Package PeopleCode
           ELSE PROJ.OBJECTVALUE1
       END AS OBJECT_NAME 
/*       
--,PROJ.OBJECTTYPE
--,PROJ.OBJECTID1
--,PROJ.OBJECTVALUE1
--,PROJ.OBJECTID2
--,PROJ.OBJECTVALUE2
--,PROJ.OBJECTID3
--,PROJ.OBJECTVALUE3
--,PROJ.OBJECTID4
--,PROJ.OBJECTVALUE4
*/
,
    CASE PROJ.SOURCESTATUS
        WHEN 0 THEN 'Unknown     '
        WHEN 1 THEN 'Absent      '
        WHEN 2 THEN 'Changed     '
        WHEN 3 THEN 'Unchanged   '
        WHEN 4 THEN '*Changed    '
        WHEN 5 THEN '*Unchanged  '
        WHEN 6 THEN 'Same        '
    END AS SOURCE_STATUS ,
    CASE PROJ.TARGETSTATUS
        WHEN 0 THEN 'Unknown     '
        WHEN 1 THEN 'Absent      '
        WHEN 2 THEN 'Changed     '
        WHEN 3 THEN 'Unchanged   '
        WHEN 4 THEN '*Changed    '
        WHEN 5 THEN '*Unchanged  '
        WHEN 6 THEN 'Same        '
    END AS TARGET_STATUS
FROM PSPROJECTDEFN PROJD ,
     PSPROJECTITEM PROJ
WHERE PROJD.PROJECTNAME = PROJ.PROJECTNAME 
AND PROJD.PROJECTNAME = @projectName
/*
--criteria for Recustomization
--  AND PROJ.SOURCESTATUS IN ('4', '5')
--  AND PROJ.TARGETSTATUS NOT IN ('0','1')
*/  		
```