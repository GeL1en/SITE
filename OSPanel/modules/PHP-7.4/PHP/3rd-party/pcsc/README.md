# PC/SC for PHP

## About

This is the only extension for using [PC/SC](http://www.pcscworkgroup.com/) based smart cards with [PHP](http://www.php.net). It is a wrapper to the wonderful and free project by Ludovic Rousseau, [PCSC-Lite](https://pcsclite.apdu.fr/), which is the middleware to access a smart card using SCard API (PC/SC). Since PCSC-Lite is compatible to the winscard API it should be possible to compile this extension using a Windows or macOS operating system.

Thanks are going to Johann Dantant! He provided a PC/SC extension for PHP since 2005 and I reused some of his code. He allowed me to relicense these parts under the terms of the PHP license so I could integrate PCSC-Lite native into PHP.

## Installation

I recommend to install the PECL extension the "PHP" way:

```
pecl install pcsc-beta
```

You can install the latest code by downloading the sources and compile yourself too.

```
git clone https://github.com/pcsc-for-php/pcsc.git
cd pcsc
phpize
./configure
make
make install
```

After that you have all needed files in ./modules/ .

## API

The extension currently provides the following API:

### scard_establish_context">scard_establish_context();

Returns the application $context to the PC/SC resource manager.

### scard_is_valid_context">scard_is_valid_context($context);

Returns TRUE if $context is valid or FALSE if $context is not valid.

### scard_release_context">scard_release_context($context);

Releases the application $context.

### scard_list_readers">scard_list_readers($context);

Returns an array of available readers or FALSE.

#### Example:

```
array(3) {
  [0]=>
  string(26) "OMNIKEY CardMan 5x21 00 00"
  [1]=>
  string(26) "OMNIKEY CardMan 5x21 00 01"
  [2]=>
  string(76) "SCL01x Contactless Reader [SCL01x Contactless Reader] (21161009200722) 00 00"
}
```

### scard_connect">scard_connect($context, "OMNIKEY CardMan 5x21 00 00");

Connects to a card. Returns the $connection to a reader or FALSE.

### scard_reconnect">scard_reconnect($connection);

Returns the $connection to a reader or FALSE.

### scard_disconnect">scard_disconnect($connection);

Disconnects the $connection to a card. Returns the TRUE if disconnecting was succesful or FALSE.

### scard_transmit">scard_transmit($connection, $apdu);

Returns the response $apdu as string or FALSE.

### scard_status">scard_status($connection);

Returns the status or FALSE.

### scard_cancel">scard_cancel($context);

## License

This code is licensed under the terms of the PHP License version 3.01. PCSC-Lite is licensed in a way where it is possible to integrate it native in the PHP environment.

## Links

 * [PECL Project Page](http://pecl.php.net/package/pcsc) - Page for package download at PHP.net
 * [PC/SC Worgroup](http://www.pcscworkgroup.com/) - Homepage and definition file downloads
 * [PC/SC](http://en.wikipedia.org/wiki/PC/SC) - PC/SC at Wikipedia
 * [PC/SC-Lite](https://pcsclite.apdu.fr/) - The free and open implementation of the PC/SC SCard API for UNIX
 * [PCSC sample in PHP5](http://ludovicrousseau.blogspot.de/2015/01/pcsc-sample-in-php5.html) - Ludovic Rousseau about "PC/SC for PHP"

