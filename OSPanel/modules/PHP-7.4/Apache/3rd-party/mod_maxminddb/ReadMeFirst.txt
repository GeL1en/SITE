  
  April 20, 2021
                           Apache Haus Distribution
                        
  Application:       mod_maxminddb 1.1.0 for Apache 2.4.x VC15
  Distribution File: mod_maxmind-1.1.0.132-2.4.x-x64-vc15
 
  Original Home: https://www.maxmind.com
  Win64 binary by: Gregg
  Mail: info@apachehaus.com
  Home: http://www.apachehaus.com


  Module Version: 1.1.0
  Maxmind dbAPI:  1.3.2


  Includes:

  Changes.txt
  GeoLite2-Country.mmdb   # GeoLite2 Country Database
  LICENSE.txt
  mod_maxminddb.so        # Apache module
  README.txt
  ReadMeFirst.txt         # This file


  ** This build for Apache 2.4.x VC14 x64 only! **

 
  # Notes:

  Modules built on Visual C++ 2015 do not run on Windows XP or Windows Server 2003

  The module is built with Visual Studio® 2015 x64, be sure to install the 
  latest Visual C++ 2015-2019 x64 Redistributable Package, download from;

  https://aka.ms/vs/16/release/VC_redist.x64.exe

  Note: x64 Windows users should install both x86 & x64 redistributables


  #Databases

  You need to obtain a maxmind database from the URL below.
  Databases are updated monthly and there are free and paid versions.

  You can get the latest databases from
  https://dev.maxmind.com/geoip/geoip2/geolite2/

  # Install:

  Copy mod_maxminddb.so to your Apache 2.4.x modules folder
  .../Apache24/modules/mod_maxminddb.so

  Install the Visual C++ 2015 x86 Redistributable Package 
  Download, if you have not done so already, from the address above.

   # Add to your httpd.conf:

	LoadModule maxminddb_module modules/mod_maxminddb.so

	# Minimal Configuration below. For a more complete configuration,
	# see included httpd-maxmind.conf

    MaxMindDBEnable On
    MaxMindDBFile COUNTRY_DB conf/etc/GeoLite2-Country.mmdb

    MaxMindDBEnv MM_COUNTRY_CODE COUNTRY_DB/country/iso_code
    MaxMindDBEnv MM_COUNTRY_NAME COUNTRY_DB/country/names/en

  # Blocking by Country #

    SetEnvIf MM_COUNTRY_CODE ^(RU|US|UK) BlockCountry
    <RequireAll>
      Require all granted
      Require not env BlockCountry
    </RequireAll>

 