# Reproduction of TypeScript memory spike from v5.5.4 to v5.6.2

Typescript uses 2x the memory for this example when upgrading from `v5.5.4` to `5.6.2`. In a real world example I saw TS memory balloon from `4GB` to `20GB`. 

The issue seems to stem from the way these TS versions handle the error `The inferred type of this node exceeds the maximum length the compiler will serialize. An explicit type annotation is needed.`

Earlier versions of TS handled this error with less memory. The newer versions handles this error less gracefully. 


Reproduction steps after cloning repo:

```
yarn install

yarn tsc -p tsconfig.app.json --declaration --emitDeclarationOnly --extendedDiagnostics

yarn add -D typescript@5.6.2

yarn tsc -p tsconfig.app.json --declaration --emitDeclarationOnly --extendedDiagnostics
```


## Typescript 5.5.4 results

```
Files:                          72
...
Memory used:               273168K
...
Total time:                  0.72s
```

## Typescript 5.6.2 results

```
Files:                          72
...
Instantiations:               2097
Memory used:               542298K
...
Total time:                  0.98s
```


