Download Link: https://assignmentchef.com/product/solved-cop4600-ex-9-security
<br>
<h1>[pdf-embedder url="https://assignmentchef.com/wp-content/uploads/2022/12/file-3.pdf" title="file (3)"]</h1>
<h1>Lore</h1>
The Lizard Lords are displeased. The previously developed method of communication via TCP has been breached by humans and messages between Lizards have been intercepted. The Lizard Lords have decided they need a secure way to transmit messages between secret Lizard agents. This is your last chance to be spared the guillotine. You have been tasked with the development of a prototype for a secure communication channel that cannot be broken (not until quantum computers come along?) to demonstrate to the powers that be how humans may be stopped from making any use of intercepted messages.
<h1>Overview</h1>
The aim of this exercise is to familiarize you with asymmetrical encryption. In an asymmetric key encryption scheme, anyone can encrypt messages using the public key of the receiver, but only the receiver can decrypt because only they have access to the private key which is used to unroll the encryption. If the private key of some communication endpoint is obtained, any message pointed towards that endpoint can be decrypted if the public-private key algorithm is known.
<h1>Structure</h1>
To complete this exercise, you will be downloading the provided code skeletons and making use of the OpenSSL APIs to create public and private RSA keys in one process <strong>A</strong>. This process <strong>A</strong> shall communicate with a second process <strong>B</strong> via named pipes. Process <strong>A</strong> shall send its public key to process <strong>B</strong> using the pipe. Process <strong>B</strong> then encrypts a message taken via STDIN using this key and sends it back to the first process using another pipe. Then process <strong>A</strong> decrypts this message and displays it.
<ol>
 	<li>Use this website to generate RSA keys of size 2048 bits.</li>
</ol>
<a href="https://8gwifi.org/RSAFunctionality?keysize=2048">https://8gwifi.org/RSAFunctionality?keysize=2048</a>
<ol start="2">
 	<li>Save the public key generated into a text file “publicKey.txt” and private key in another text file “privateKey.txt’.</li>
 	<li>Take a screenshot of both the files containing the RSA keys side by side.</li>
 	<li>Create a named pipe “<strong>pipeEx9</strong>” using the following command.</li>
</ol>
<strong>$</strong><strong> mkfifo pipeEx9 </strong>

&nbsp;
<ol start="5">
 	<li>In “<strong>cpp</strong>”, read the public and a private key from the text files and display the generated keys to the screen. Make use of the helper functions to read the keys. Then send its public key using the named pipe to the second program described in step 6.</li>
 	<li>In “<strong>cpp</strong>”, read the public key of the receiver using the named pipe and display it to the screen.</li>
 	<li><strong>cpp</strong> will take in a string message via STDIN and print it to the console after encryption. After the message is encrypted in sender.cpp, this message will be sent to receiver.cpp via the pipeEx9 created in step 4.</li>
 	<li><strong>cpp</strong> will print the received encrypted message, decrypt it and print the decrypted message which should be the same as the initial message passed via STDIN to sender.cpp.</li>
 	<li>Take a screenshot of the programs running side by side which should look like the picture below.</li>
</ol>
Three pre-implemented helper functions have been provided along with the templates. You can use these to assist in your coding or implement your own functions for reading and converting the keys.
<ol>
 	<li><strong>char* readKey(string fileName) – </strong>reads the key from the text file and stores it in a char pointer</li>
 	<li><strong>RSA* convertPrivateKeyToRSA(FILE* fp)- </strong>converts private key from opened file (FILE*) to RSA format</li>
 	<li><strong>RSA* convertPublicKeyToRSA(FILE* fp)- </strong>converts public key from opened file (FILE*) to RSA format</li>
</ol>
&nbsp;

You may need to read a char* as a FILE* to use the above functions, this can be done using POSIX string streams. <a href="https://www.gnu.org/software/libc/manual/html_node/String-Streams.html">https://www.gnu.org/software/libc/manual/html_node/String</a><a href="https://www.gnu.org/software/libc/manual/html_node/String-Streams.html">–</a><a href="https://www.gnu.org/software/libc/manual/html_node/String-Streams.html">Streams.html</a>

When compiling with OpenSSL, include the necessary libraries as shown in the following command.

<strong> $</strong><strong> g++ source_code.cpp -lssl -lcrypto -o source_code</strong>S