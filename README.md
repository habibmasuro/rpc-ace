RPC Ace (RPC AnyCoin Explorer)
==============================

Copyright (c) 2014 Robin Leffmann

RPC Ace is a simple alternative block explorer written in PHP. It does not generate a database, and it interacts with block chains entirely via RPC, either against a locally running wallet/daemon or remotely over the Internet.

A database-less explorer has a few drawbacks - most notably, RPC Ace cannot keep track of addresses or total coins generated, and as it uses RPC calls to parse blocks a transaction-heavy block chain (such as Bitcoin) can incur heavy CPU usage and/or long page generation times. RPC Ace's primary use is quick access to oversight of a block chain; for in-depth needs it's recommended to run a tallying explorer such as Abe.

RPC Ace should work with any block chain regardless of what proof-of-work algorithm is used, and has been tested to work with Bitcoin, Litecoin, Dogecoin, Solcoin and a few other block chains, but as it's still at an early stage it may contain bugs. Version 0.6.5 introduced PoS support, which has been tested against a number of popular PoS block chains.


Setting up RPC Ace
------------------

RPC Ace (and the extras) requires PHP version 5.4 or later, with CURL and JSON support enabled.

Place `rpcace.php` and `easybitcoin.php` ([get it here](https://github.com/aceat64/EasyBitcoin-PHP)) together in your web directory. The first few lines of `rpcace.php` contain all of its configurable parameters:

    $rpcHost = '127.0.0.1';                  // Host/IP for the daemon
    $rpcPort = 12345;                        // RPC port for the daemon
    $rpcUser = 'username';                   // 'rpcuser' from the coin's .conf
    $rpcPass = 'password';                   // 'rpcpassword' from the coin's .conf
    $coinName = 'Somecoin';                  // Coin name/title for the explorer
    $coinHome = 'http://www.somecoin.org/';  // Coin website
    $coinPoS = false;                        // Set to true for proof-of-stake coins
    $numBlocksPerPage = 12;                  // Number of blocks to parse per page
    $refreshTime = 180;                      // Seconds between automatic page refresh


To get accurate transaction values your block chain must be built with full transaction indexing from the start, by setting `txindex=1` in the coin's .conf file.


Extras
------

`tally.php` generates a "rich list". Usage: configure user/pass/host/port in the beginning of the file, and then run from command line: `php tally.php <output>`. Accurate results require the block chain being built with full transaction indexing. Avoid storing `tally.php` in your web directory where users may run it remotely, as it can be very time- and CPU-consuming when parsing long block chains.

When finished parsing blocks, `tally.php` will output its progress to a file named `RPCUSER-RPCPORT-tally.dat` which will be used to resume operations next time `tally.php` runs in order to avoid having to start over from block 1 when updating a list. Aborting the script while running by pressing `CTRL+C` will also save the progress file for later use.


Donations
---------

BTC: 1EDhbo9ejdKUxNW3GPBh1UmocC1ea1TvE5  
LTC: LaDuRFwEt1V26pmJJH94auDvxqN3rRFqPj  
DOGE: DK2pB2XXQ9w13UZD2J9wsEHFVDvuE767wT  
VTC: VwDmyMR5udPkEwTJhxDsUB2C3mk8NKCSD8  
DRK: XvHfibq2f1xU6rYqAULVXHLPuRhBawzTZs  


License
-------

RPC Ace is released under the Creative Commons BY-NC-SA 4.0 license: http://creativecommons.org/licenses/by-nc-sa/4.0/
