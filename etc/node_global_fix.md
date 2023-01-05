# How to npm audit global packages 
<br/>

## environment
mac <br/>
node version 15 installed<br/>
<br/>

## try
```
npm audit fix -g
```
-> 🚫Audit not applied to global
<br/><br/>

## Solutions✨
Navigate directly to the global package location and run npm audit

```
cd ~/.nvm/versions/node/[node_version]/lib/node_modules
npm audit fix 
```
