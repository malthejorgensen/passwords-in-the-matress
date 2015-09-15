Passwords in the mattress
=========================
Password manager written in Elm

To do
-----
- [ ] User should be able to add passwords
- [ ] User should be able to change passwords
- [ ] User should be able to delete passwords
- [ ] Save encrypted password JSON object in LocalStorage
- [ ] Never show password before user requests it
- [ ] When password is not shown, it should be encrypted (this effectively means that passwords are double encrypted)
      such that passwords aren't plaintext in memory, until user requests to view the password.  
      (Note: The passwords will be able to be decrypted given that the attacker locates the key in memory)
- [ ] Send encrypted password JSON object to specified REST endpoint
- [ ] Use [JSON Schema](http://json-schema.org/) to describe password file format.
- [ ] User should be able to add a note to each password (in Markdown)
- [ ] The interface should be usable on a smartphone
- [ ] (in the non-near future) Ensure that pitm lives up to the attacks described in
       <https://www.cs.ox.ac.uk/files/6487/pwvault.pdf>


Doubly encrypted password
-------------------------
_Not implemented yet_

To deter attackers from stealing passwords by inspecting the memory of the user's computer,
PITM tries not to store passwords in plaintext in memory unless stricly necessarry.
This means that password are encrypted "twice": First you need to decrypt to full PITM JSON object
with the master password, then you need to decrypt each individual password with a hash of the
master password (so that the master password isn't stored in memory) and the nonce for the given
password.

    derived_key = HASH_FUNC(master_password + nonce_for_json_file)
    plaintext_password = decrypt(HASH_FUNC(derived_key + nonce_for_password), encrypted_password)

