TA-Microsoft-Sysmon v0.3.1
----------------------------	
	
	Author: ahall (original). japger, dherrald, jbrodsky (update).
	Version/Date: 0.3.1 09/28/2015
	Sourcetype: XmlWinEventLog:Microsoft-Windows-Sysmon/Operational
	Has index-time ops: false
	Input Requirements: Sysmon 3.1 installed on Windows UF

Updates 
----------------------------

	0.3.1
	-----
	Lookup table added to support Sysmon 3.1
	Additional CIM compliance added
	Example config added
	Revved to version 0.3.1 to match current Sysmon version


Using this TA
----------------------------

	Configuration: Install TA via GUI on all search heads, install
	via your preferred method (manual or Deployment Server) on
	forwarders running on Windows that have Sysmon 3.1 or greater
	installed

	Ensure that you have at least version 6.2.0 universal forwarders.
	This is because of the Windows XML event log format.

http://blogs.splunk.com/2014/11/04/splunk-6-2-feature-overview-xml-event-logs/

	For additional info on Sysmon see here:

http://blogs.splunk.com/2014/11/24/monitoring-network-traffic-with-sysmon-and-splunk/

Support
----------------------------

	This is a community supported TA. As such, post to answers.splunk.com
	and reference it. Someone should be with you shortly.

Example Config
----------------------------

	Sysmon is capable of delivering a large amount of events into your
	Splunk instance. The following configuration, loaded into each
	system running Sysmon 3.1, will reduce the amount of data considerably.
	Special thanks go to Jeff Walzer from the University of Pittsburgh for
	helping to test this (walzer@pitt.edu).

	Load this via sysmon -c (filename) from an admin-level command prompt.
	(after you have placed it in a text file). You may get some 
	unusual errors - these are benign and can be ignored. Check the
	filtering via a "sysmon -c" with no argument.

	For additional Sysmon filtering, remove the entire ImageLoad 
	section.

**** CUT HERE ****

<Sysmon schemaversion="2.0">
  <HashAlgorithms>SHA1</HashAlgorithms>
  <EventFiltering>
		<!-- Log all drivers except if the signature -->
		<!-- contains Microsoft or Windows -->
	<DriverLoad onmatch="exclude">
		<Signature condition="contains">microsoft</Signature>
		<Signature condition="contains">windows</Signature>
	</DriverLoad>
    	<!-- Exclude certain processes that cause high event volumes -->
   	<ProcessCreate default="include">
		<Image condition="contains">splunk</Image>
        	<Image condition="contains">streamfwd</Image>
        	<Image condition="contains">splunkd</Image>
		<Image condition="contains">splunkD</Image>
		<Image condition="contains">splunk</Image>
		<Image condition="contains">splunk-optimize</Image>
		<Image condition="contains">splunk-MonitorNoHandle</Image>
		<Image condition="contains">splunk-admon</Image>
		<Image condition="contains">splunk-netmon</Image>
		<Image condition="contains">splunk-regmon</Image>
		<Image condition="contains">splunk-winprintmon</Image>
		<Image condition="contains">btool</Image>
		<Image condition="contains">PYTHON</Image>
	</ProcessCreate>
	<ProcessTerminate default="include">
		<Image condition="contains">splunk</Image>
		<Image condition="contains">streamfwd</Image>
		<Image condition="contains">splunkd</Image>
		<Image condition="contains">splunkD</Image>
		<Image condition="contains">splunk</Image>
		<Image condition="contains">splunk-optimize</Image>
		<Image condition="contains">splunk-MonitorNoHandle</Image>
		<Image condition="contains">splunk-admon</Image>
		<Image condition="contains">splunk-netmon</Image>
		<Image condition="contains">splunk-regmon</Image>
		<Image condition="contains">splunk-winprintmon</Image>
		<Image condition="contains">btool</Image>
		<Image condition="contains">PYTHON</Image>
	</ProcessTerminate>
	<FileCreateTime default="include">
		<Image condition="contains">splunk</Image>
		<Image condition="contains">streamfwd</Image>
		<Image condition="contains">splunkd</Image>
		<Image condition="contains">splunkD</Image>
		<Image condition="contains">splunk</Image>
		<Image condition="contains">splunk-optimize</Image>
		<Image condition="contains">splunk-MonitorNoHandle</Image>
		<Image condition="contains">splunk-admon</Image>
		<Image condition="contains">splunk-netmon</Image>
		<Image condition="contains">splunk-regmon</Image>
		<Image condition="contains">splunk-winprintmon</Image>
		<Image condition="contains">btool</Image>
		<Image condition="contains">PYTHON</Image>
    	</FileCreateTime>
	<ImageLoad default="include">
		<Image condition="contains">splunk</Image>
		<Image condition="contains">streamfwd</Image>
		<Image condition="contains">splunkd</Image>
		<Image condition="contains">splunkD</Image>
		<Image condition="contains">splunk</Image>
		<Image condition="contains">splunk-optimize</Image>
		<Image condition="contains">splunk-MonitorNoHandle</Image>
		<Image condition="contains">splunk-admon</Image>
		<Image condition="contains">splunk-netmon</Image>
		<Image condition="contains">splunk-regmon</Image>
		<Image condition="contains">splunk-winprintmon</Image>
		<Image condition="contains">btool</Image>
		<Image condition="contains">PYTHON</Image>
	</ImageLoad>
   </EventFiltering>
</Sysmon>

**** CUT HERE ****
