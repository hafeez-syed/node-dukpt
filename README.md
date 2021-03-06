# node-dukpt

[![npm version](https://badge.fury.io/js/dukpt.svg)](https://badge.fury.io/js/dukpt) ![alt tag](https://api.travis-ci.org/dpjayasekara/node-dukpt.svg?branch=master) ![alt dependencies](https://david-dm.org/dpjayasekara/node-dukpt.svg) ![alt dev-dependencies](https://david-dm.org/dpjayasekara/node-dukpt/dev-status.svg) [![Coverage Status](https://coveralls.io/repos/github/dpjayasekara/node-dukpt/badge.svg)](https://coveralls.io/github/dpjayasekara/node-dukpt) [![Code Climate](https://codeclimate.com/github/dpjayasekara/node-dukpt/badges/gpa.svg)](https://codeclimate.com/github/dpjayasekara/node-dukpt)


##Derived Unique Key Per Transaction (DUKPT) Encryption with NodeJS

This the NodeJS implementation of DUKPT based on the vanilla javascript implementation of **IDTech** DUKPT encryption/decryption. Don't hesitate to report any bugs in the [Github Repository!](https://github.com/dpjayasekara/node-dukpt).

Many thanks to @jamiesoncj for providing resources.

### Installing

```
npm install dukpt --save
```
### Using DUKPT

Initialize DUKPT by providing BDK and KSN:

```
const Dukpt = require('dukpt');

const encryptionBDK = '0123456789ABCDEFFEDCBA9876543210;
const ksn = 'FFFF9876543210E00008';
const encryptedCardData = '411D405D7DEDB9D84797F04<redacted_for_brevity>050509277E5F80BE67A2C324900A7E3';
const plainTextCardData = '%B5452310551227189^DOE/JOHN      ^08043210000000725000000?';

const dukpt = new Dukpt(encryptionBDK, ksn);
```
After initializing, you can use `dukptEncrypt` and `dukptDecrypt` methods to encrypt/decrypt data using DUKPT. 

#### Encrypting `ascii` data

```
const options = {
	inputEncoding: 'ascii', 
	outputEncoding: 'hex',
	encryptionMode: '3DES'
};
const encryptedCardData = dukpt.dukptEncrypt(plainTextCardData, options);
```

#### Encrypting `hex` data

```
const options = {
	inputEncoding: 'hex',
	outputEncoding: 'hex',
	encryptionMode: '3DES'
};
const encryptedCardData = dukpt.dukptEncrypt(plainTextCardData, options);
```

#### Decrypting data with `ascii` output encoding

```
const options = {
	outputEncoding: 'ascii',
	decryptionMode: '3DES',
	trimOutput: true
};

const decryptedCardData = dukpt.dukptDecrypt(encryptedCardData, options);
```
#### Decrypting data with `hex` output encoding

```
const options = {
	outputEncoding: 'hex',
	decryptionMode: '3DES',
	trimOutput: true
};

const decryptedCardData = dukpt.dukptDecrypt(encryptedCardData, options);
```

###Options

You can use options object to provide additional options for the DUKPT encryption/decryption. This object is **optional** and, if you don't provide it, encryption/decryption will use the default values shipped with it. 

Following listed are the available options.

Option | Possible Values | Default Value | Description
------------ | ------- | ------------- | --------------
`outputEncoding` | `ascii`, `hex` | For encryption `hex`, for decryption `ascii` | Specify output encoding of encryption/decryption
`inputEncoding` | `ascii`, `hex` | For encryption `ascii`, for decryption `hex` | Specify encoding of the input data for encryption/decryption
`trimOutput` (for decryption only) | `true`, `false` | `false` | Specify whether to strip out null characters from the decrypted output
`encryptionMode` (for encryption only) | `3DES` | `3DES` | Specify encryption scheme for dukpt
`decryptionMode` (for decryption only) | `3DES` | `3DES` | Specify decryption scheme for dukpt

* Support for AES encryption/decryption mode will be added soon!

###Tests
Tests can be run using gulp as follows:

```
gulp test
```

####Roadmap

- [x] Support for DUKPT Encryption/Decryption with 3DES
- [ ] Support for DUKPT Encryption/Decryption with AES


