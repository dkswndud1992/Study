# How to npm audit global packages

## environment
mac 
node version 15 installed


## try
```
npm audit fix -g
```
-> 🚫Audit not applied to global


## Solutions✨
Navigate directly to the global package location and run npm audit

```
cd ~/.nvm/versions/node/[node_version]/lib/node_modules
npm audit fix 
```
