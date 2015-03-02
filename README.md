# MetasploitPenTestScript

This is a ruby gem that basically wraps the msfrpc-client gem. 

It was primarily created to automate workspace creation and automatic import of nexpose scan data from use in 
a Jenkins automated CI/CD environment. 

Basically this allows you to attach metasploit to your Continuous Delivery/Continuous integration pipeline. 
Though it can be used for other purposes.

## Installation

Add this line to your application's Gemfile:

    gem 'metasploit-runner'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install metasploit-runner

## Usage

This gem allows you to specify the Metasploit Connection URL, Metasploit Connection Port, Metasploit URI, SSL true/false, Token, Workspace Name, Nexpose Console Name, Device/Target IP, and Exploit Module OS Filter.

The nexpose_console_name is optional, if you specify a nexpose console name it will use the workspace_name, and nexpose console name to pull scan data from a nexpose console.
IMPORTANT: Your "Site Name" in Nexpose, must match your "Workspace" name in Metasploit and you must add your Nexpose Console to Metasploit for this to work properly.

    $ exploit "connection_url" "port" "uri" "use_ssl" "token" "workspace_name" "nexpose_console_name" "device_ip_to_scan" "os_filter" "module_filter" "report_type"

Example WITH Nexpose Console Integration:

    $ exploit "sploit.mydomain.com" "3790" "/api/1.0" "<true/false>" "asdlkjhsdfuw1228340asdasf8" "mycoolsoftware-build-28" "nexpose-console-1" "10.0.0.1" "<true/false>" "exploit/windows/smb/psexec" "fisma"

Example WITHOUT Nexpose Console Integration:

    $ exploit "sploit.mydomain.com" "3790" "/api/1.0" "true" "asdlkjhsdfuw1228340asdasf8" "mycoolsoftware-build-28" "" "10.0.0.1" "false" "exploit/windows/smb/psexec" "fisma"

Additionally, an os filter may be passed in to determine which modules will be ran during an exploit.  The os filter parameter will default to false (all modules will run) if you do not pass a value.

    Note: at the time of publishing this version of the gem, that was over 6,000 modules, which is ALOT. This option will only work of metasploit has a high confidence in your O/S type.

Example WITH OS Filter:

    $ exploit "sploit.mydomain.com" "3790" "/api/1.0" "true" "asdlkjhsdfuw1228340asdasf8" "mycoolsoftware-build-28" "nexpose-console-1" "10.0.0.1" "true" "" "fisma"

The if you do not pass the following options they will default to the respective values:

       port -> 3790
       uri -> /api/1.0
       use_ssl -> true
       os_filter -> false

Example using the defaults:

    $ exploit "sploit.mydomain.com" "" "" "" "asdlkjhsdfuw1228340asdasf8" "mycoolsoftware-build-28" "nexpose-console-1" "10.0.0.1" "" "" ""

## Contributing

1. Fork it ( https://github.com/[my-github-username]/MetasploitPenTestScript/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
