 == Project Spring Clean ==
 
 It is time for this lirary to get updated so it is a little more modern, when it was made things were just done diffrently.
 If you have a idea, im open to impliment it... if you look at my history of acepting pull requests i have a 100% aceptance rate
 so please dont fork and run with this on your own... if you want i will just add you as a developer once you have done a few pull requests.
 
 during project Spring Clean i want to use getters for listing records, namespace the project, add a PSR-3 style logger,
 adopt PSR-1/PSR-2 and debating with myself if a trait would be handy... not sure tho its not like a file storage system, any thoughts?
 
 Rackspace DNS PHP API ...
 

 please register any issues to: https://github.com/snider/php-cloudDNS/issues/
 
 Copyright (C) 2011  Paul Lashbrook
 
 This program is free software: you can redistribute it and/or modify
 it under the terms of the GNU General Public License as published by
 the Free Software Foundation, either version 3 of the License, or
 (at your option) any later version.
 
 This program is distributed in the hope that it will be useful,
 but WITHOUT ANY WARRANTY; without even the implied warranty of
 MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 GNU General Public License for more details.
 
 You should have received a copy of the GNU General Public License
 along with this program.  If not, see <http://www.gnu.org/licenses/gpl-3.0.txt>.
 
 @author      Paul Lashbrook

 @contributor Alon Ben David @ CoolGeex.com
 @contributor zeut @ GitHub - reported a fix for limiting... totally forgot that bit!
 @contributor idfbobby @ github - updated the create_domain() function to include comments and ttl
 @contributor diegoiglesias @ github - updated authentication code to cater for new style accounts.

CHANGES 

27/3/2012 Reported by Zeut
- fixed a ssl peer veify error for people with old versions of curl
	

26/3/2012 Reported by Zeut, fixed by Paul Lashbrook
- Updated php Docs
- Added pagination
     list_domains()
     list_subdomains()
     list_records()
     list_domain_search()
     list_domain_details()
- search_domains alias added


 08/09/2011 Paul Lashbrook
- added import_domain()
- added alias function delete_domain()
- relaxed data type checking
- fixed callback waiting until timeout


30/08/2011 Alon Ben David @ CoolGeex.com
- Class name now rackDNS
- callback function to cycle through registered call backs with timeout in place
- Added support to US rackspace DNS API
- delete_domain Now called delete_domains (accept int for one domain OR array for multiple domains)
- added modify_domain function to modify domain configuration
- added domain_import function to import BIND9 format string
- created a sample.php file with code samples


PHP API binding to Rackspace Cloud DNS (US & UK)
-----------------------------------------
This is strictly for PHP5 since PHP4 should be forgotten forever.

PLEASE NOTE: any help suggestions/requests welcome

Server communication code originally from and slightly adapted,
thanks to the work of that author making this was relatively easy

you made get errors trying to establish an ssl conection to rackspace,
if you get this you have a old version of Curl installed meaning the CA list is outdated.

just run $dns->set_cabundle(true); before you try to do a API action

@link http://snider.github.com/php-cloudDNS/
via https://github.com/eyecreate/Rackspace-Cloud-PHP-Library

All API Methods Implemented So Far: Check sample.php for code sample

$dns = new rackDNS($rs_user,$rs_api_key); //($user, $key, $endpoint = 'UK') $endpoint can be UK or US

// Show all domains avalible
$dns->list_domains(50,0); //($limit = 10, $offset = 0)

$dns->list_subdomains($sampleID);//($domainID)

$dns->domain_export($sampleID);//($domainID)

$dns->list_records($sampleID);//($domainID)

$dns->list_record_details($sampleID,$recID);//($domainID,$recordID)

$dns->domain_import($sampleImport);

$dns->list_domain_search('domain.com');

$dns->modify_domain($sampleID,'info@domain.com'); //($domainID = false , $email = false , $ttl = 86400 , $comment = 'Modify Domain Using rackDNS API')

$dns->delete_domains($sampleID);

$dns->delete_domain_record($domainID,$recordID)

$dns->list_domain_details($domainID = false, $showRecords = false, $showSubdomains = false);


$dns->import_domain('domain.com');

$dns->create_domain($name = false, $email = false, $records = array());

$dns->create_domain_record($domainID = false, $records = array());

$dns->create_domain_record_helper($type = false, $name = false, $data = false, $ttl = 86400, $priority = false);

example use:

$dns = new rackDNS(RS_USER,RS_API_KEY);

// make a new dns zone
  $records = array($dns->create_domain_record_helper('MX','originalwebware.com','mail.originalwebware.com',86400,2),
  					$dns->create_domain_record_helper('a','originalwebware.com','192.168.0.1',86400));
  name, email, comment, ttl, records
  $results = $dns->create_domain('originalwebware.com', 'paul@originalwebware.com', 'a comment', 3600, $records);
 
 // add a new record(s) to a dns zone
  $records = array($dns->create_domain_record_helper('MX','originalwebware.co.uk','mail.originalwebware.co.uk',86400,2),
 					$dns->create_domain_record_helper('a','originalwebware.co.uk','192.168.0.1',86400));
 $results = $dns->create_domain_record(123456,$records);
 



$dns->getLastResponseStatus(); //returns status code
$dns->getLastResponseMessage();//returns status message
