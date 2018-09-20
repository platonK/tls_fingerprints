# Client Application TLS Fingerprints
TLS client fingerprints used in our IMC 2018 paper.
> Platon Kotzias, Abbas Razaghpanah, Johanna Amann, Kenneth G. Paterson, Narseo Vallina-Rodriguez, and Juan Caballero. 
Coming of Age: A Longitudinal Study of TLS Deployment. 
In Proceedings of the Internet Measurement Conference (IMC), October 2018.

A TLS fingerprint is the concatenation of four features extracted from the Client Hello:
1. cipher suite list,
2. client extensions list,
3. Supported Elliptic Curves (EC)
4. Supported EC Point Formats extension. 

All features are stored represented with their codes (as integers) and in the order they appear in the Client Hello.

Each fingerprint maps to one program or library version. 
Our collection contains 4,419 entries (1,684 fingerprint).
Multiple entries may have the same TLS fingerprint for different reasons.
This can be because various versions of the same application share the same TLS fingerprint (e.g., Firefox 10,11,12),
applications may use a known TLS library (e.g., Android and iOS apps), and finally because two (or more) applications just happen to have the same fingerprint. The latter category has been excluded from our IMC '18 work but included it here because it may be useful for other types of usage/research.

Each line in the tls_fprints.jsons is a JSON with the following structure:
- description:  A string that describes the application as "app_name;app_version;os;os_version;architecture;comments"
- fprint: The TLS fingerprint as a string with the following structure "client_cipher_suite_list;client_extension_list;supported_elliptic_curves;supported_ec_point_formats"
- fprint_md5: An MD5 hash of the fprint field

An example of a TLS fingerprint:

>{"description": "firefox;30.0;windows;8.1;;", "fprint_md5": "9ef88fc204ff6564546cf7777986d358", "fprint": "49195,49199,49162,49161,49171,49172,49170,49159,49169,51,50,69,57,56,136,22,47,65,53,132,10,5,4;0,65281,10,11,35,13172,5,13;23,24,25;0"}


Some Google software like Chrome uses a feature called [GREASE](https://tools.ietf.org/html/draft-davidben-tls-grease-01) that adds a list of invalid values to various fields in the TLS handshake to improve server tolerance of future new extensions.
We identify GREASE codes in our features, remove them, and append a GREASE string at the end of the affected feature. An example can be seen here:

>{"description": "chrome;55.0;macos;high sierra;;", "fprint_md5": "d667ae2d99d2beb19b32474bf9da0616", "fprint": "49195,49199,49196,49200,52393,52392,52244,52243,49161,49171,49162,49172,156,157,47,53,10,GREASE;65281,0,23,35,13,5,18,16,30032,11,10,GREASE;29,23,24,GREASE;0"}


**Collection methods**

We collected our TLS fingerprints using various methods:

- Using the BrowserStack, a cloud based web and mobile testing platform, for browsers and mobile devices TLS fingerprints.
- Compiled multiple versions of TLS libraries (e.g., OpenSSL)
- Executed Malware and PUP samples with TLS communication
- Android SDK and applications [from prior work on Android TLS usage](http://www.icir.org/johanna/papers/conext17android.pdf)
- Incorporated parts of other puclicly available TLS fingerprint datasets:
   - AV and proxy fingerprints [from prior work on HTTPS Interception](https://jhalderm.com/pub/papers/interception-ndss17.pdf)
   - [Lee Brotherston](https://github.com/synackpse/tls-fingerprinting) TLS fingerprint collection


