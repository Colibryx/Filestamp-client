# Filestamp Official Client

The Filestamp Official Client is a tool that allows you to decrypt crypted files uploaded on the blockchain using the Filestamp web application. It provides a certificate of timestamping that indicates when the file was created.

This client is written in Tauri and comes with pre-compiled executables that can be downloaded from the GitHub releases page. The client is open source to provide transparency to the user.

## What is filestamp?
Filestamp is a cutting-edge web application that enables you to timestamp your valuable files on the blockchain, providing a secure certificate of timestamping that verifies the precise moment your file was created. This certificate is a PDF document that includes critical information such as the password to decrypt the file, the ID of the NFT associated with the uploaded file, and the file link. To ensure maximum security, the file is encrypted using AES-256-CBC algorithm, and the password is the hash of the file. The file is then uploaded on the IPFS network, and the hash of the file is stored on the blockchain. Finally, the NFT is minted on the Algorand blockchain, providing an additional layer of protection for your valuable files. Learn more about Filestamp on our [website](https://filestamp.app).

## Features

- Decrypt AES-256-CBC Encrypted files.

## Installation

To install the Filestamp Official Client, follow these steps:

1. Go to the [GitHub releases page](https://github.com/filestamp/filestamp-official-client/releases).
2. Download the appropriate executable for your platform.
3. Run the executable.

## Usage
1. Open the client.
2. Select the file you want to decrypt.
3. Insert the passphrase given in your pdf certificate.
4. Click on the "Decrypt" button.

## License

The official client is open source under the [GPL3 License](LICENSE).

## Credits

Filestamp is proudly developed by [Colibryx](https://colibryx.com).