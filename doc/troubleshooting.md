## I can't access Rockside localhost interface via https in dev mode on Chrome/Chromium on Linux

Rockside generates a self-signed certificate which is interpreted as an invalid certificate on Chrome.
You can enable loading invalid certificates from localhost by typing 'chrome://flags/#allow-insecure-localhost' in your browser. Do this trick in development mode only. Then you can access https://localhost:443 (or any port you specified during the setup) on Chrome.

## My Parity node has been launched more than one hour ago and 'current block' is still 0. Is it working?

Parity fast sync process downloads and initializes snapshots. It could take a long time (more than one hour) to begin to synchronize the first block, especially if you run other processes on the same server.
