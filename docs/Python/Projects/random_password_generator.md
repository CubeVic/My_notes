# Random password generator - Project Davinci

The password generator project, Code *Davinci* is a random generator base in built-in library `secrets`.

The idea is to generate random password following the good practice:
* Lower and Upper case Characters.
* Digits.
* Punctuation marks.

 by default it will generate a 8 character password but in the future version it will allow generate longer passwords.

> The frist version will ask for the length of the password by terminal/console and give back the random generated password, future version will have a GUI.
```python
import string
import secrets

def pass_generator(size: int) -> str:
	alphabet = string.ascii_letters + string.digits + string.punctuation
	while True:
		password = ''.join(secrets.choice(alphabet) for i in range(size))
		if (any(c.islower() for c in password) and
			any(c.isupper() for c in password) and
			sum(c.isdigit() for c in password) )>= size//2:
			break
	return password

if __name__ == "__main__":
	while True:
		try:
			size = int(input("input password size: ")) or 8
			print(f'\n* Password:\n{pass_generator(size)}')
			break
		except ValueError:
			print("wrong value, please input a numeric value")

```

Project git: [https://github.com/CubeVic/Project_Davinci](https://github.com/CubeVic/Project_Davinci)
