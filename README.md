# CloudFlare::DNS::Update

This gem provides a simple executable tool for managing CloudFlare records to provide dynamic DNS like functionality. You need to add it to whatever `cron` system your host system uses.

## Installation

Install it yourself as:

	$ gem install cloudflare-dns-update

## Usage

Run the included `cloudflare-dns-update` tool and you will be walked through the configuration process. You might want to specify a specific configuration file, using the `--configuration /path/to/configuration.yml` option.

### Daily updates using CRON

Simply set up configurations for each domain you wish to update, and add to `/etc/cron.daily/dyndns`, e.g.:

	#!/usr/bin/env sh

	cloudflare-dns-update --configuration /srv/dyndns/domain.A.yml

Note that in case you want to update more than one domains in a zone with the same IP address, you can have multiple domains in a configuration file. Follow instructions of the configuration process. Just to note, each domain would be updated with the same content. Having both IPv4 and IPv6 records in the same configuration file is not possible nor recommended. Please create separate configuration files.

The configuration file would end up looking something like this:

	---
	:key: b10a8db164e0754105b7a99be72e3fe5
	:email: samuel@oriontransfer.org
	:zone: oriontransfer.co.nz
	:content_command: curl ipinfo.io/ip

### IPv6 Support

It is possible to update IPv6 when you have a dynamically allocated prefix. To get your current IPv6 address, the following command can be used:

	/sbin/ip -6 addr | awk -F '[ \t]+|/' '$3 == "::1" { next;} $3 ~ /^fe80::/ { next ; } /inet6/ {print $3}'

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License

Released under the MIT license.

Copyright, 2013, by [Samuel G. D. Williams](http://www.codeotaku.com/samuel-williams).

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
