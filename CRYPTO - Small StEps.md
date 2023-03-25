Challenge: Small StEps

Category: Crypto

Description: As you continue your journey, you must learn about the encryption method the aliens used to secure their communication from eavesdroppers. The engineering team has designed a challenge that emulates the exact parameters of the aliens' encryption system, complete with instructions and a code snippet to connect to a mock alien server. Your task is to break it.

My First Thoughts: So in this challenge, we can download files and we have a docker. My first thoughts after reading the challenge name were nothing much special except I got some hint with "small" (yea I didn't notice that uppercase "E"). After reading the title and description carefully I had a sure thought in my mind that it was RSA cube-root attack.

Solution:
I first downloaded the files and examined them. We have one file namely, server.py. The code of server.py is below:
server.py:
```
    from Crypto.Util.number import getPrime, bytes_to_long

FLAG = b"HTB{???????????????}"
assert len(FLAG) == 20


class RSA:

    def __init__(self):
        self.q = getPrime(256)
        self.p = getPrime(256)
        self.n = self.q * self.p
        self.e = 3

    def encrypt(self, plaintext):
        plaintext = bytes_to_long(plaintext)
        return pow(plaintext, self.e, self.n)


def menu():
    print('[E]ncrypt the flag.')
    print('[A]bort training.\n')
    return input('> ').upper()[0]


def main():
    print('This is the second level of training.\n')
    while True:
        rsa = RSA()
        choice = menu()

        if choice == 'E':
            encrypted_flag = rsa.encrypt(FLAG)
            print(f'\nThe public key is:\n\nN: {rsa.n}\ne: {rsa.e}\n')
            print(f'The encrypted flag is: {encrypted_flag}\n')
        elif choice == 'A':
            print('\nGoodbye\n')
            exit(-1)
        else:
            print('\nInvalid choice!\n')
            exit(-1)


if __name__ == '__main__':
    main()```
So for the people who don't do ctfs on a regular basis, This is some huge-monstrous code. So I'll do my best trying to explain RSA cube-root attack. I won't be explaining RSA here, you are free to refer to the wiki. Back to the challenge. So after seeing this code it is clear that the flag is encrypted with RSA encryption method and we have to decrypt it. After connecting to the docker with netcat we get the following values:
```N: 7249274512235074369364911603031554163337566775088465952431076772913859166556131001072260399959008388774671374166114123531305279958551781565385614776406041
e: 3

The encrypted flag is: 70407336670535933819674104208890254240063781538460394662998902860952366439176467447947737680952277637330523818962104685553250402512989897886053```
What happens in RSA Cube-root attack is that we take the cube root of the cipher text (in this case the encrypted flag) but this only works for small exponent(e) values like 3. In this case it should work because we have an exponenet value equal to 3 so let's try. After getting the cube root of the encrypted flag we get "412926389432612660984016953290834154417829082237" So this is not the flag right? But after using the bytes_to_long function of the crypto library in python we get the flag and I think that's it for this writeup.
