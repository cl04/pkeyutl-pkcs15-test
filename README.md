# pkeyutl-pkcs15-test
test openSSL pkeyutl pkcs15 sign/verify

* generate openSSL private key (2048-bit RSA, public exponent is default/65537):

``openssl genrsa -out private.key 2048``

* generate RSA public key from private key:

``openssl rsa -in private.key -outform PEM -pubout -out public.key``

* for a random file, input.bin, create a SHA256 digest by:

``openssl dgst -SHA256 -binary -out digest.bin <input.bin>``

* sign digest by ``pkeyutl``

``openssl pkeyutl -sign -inkey priate.key -in digest.bin > signature.bin``

* verify signature by ``pkeyutl``

``openssl pkeyutl -verify -inkey public.key -in digest.bin -sigfile signature.bin``

All steps must be done by python crypto libary if possible, create test cases (better generate random input.bin) to verify ``verify . sign`` == True.
Must not leave any temp files on disk even on error.
