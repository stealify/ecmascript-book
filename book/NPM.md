# NPM Package Manager shiped with NodeJS by Default

# Binary (Executeable files)
Onlinux we got a shebang to turn any file into executeable npm reads that if the file is referenced as bin in the package.json and creates on windows
a additional cmd file. https://github.com/npm/cmd-shim/blob/f59af911f1373239a7537072641d55ff882c3701/index.js#L22

# npx
npx can run any binary installed inside your project. under node_modules/.bin and also back traverses ../node_modules and so on.

## node_modules/.bin
is a special folder that does not get maintained on npm install so if you place files inside it that are not referenced by any package.json it will not touch them
every other folder under node_modules/* will not survive and will get deleted 

# npm run scripts
npm supports npm run scriptName referenced inside the package.json as rule of thumb avoid chaining inside that create bins referenced under your package.json and reference them also as npm script

this way you can run your tasks via npx task:name or npm run task:name which is the same but you can later outsource your tasks into indipendent packages and this way
later split that up so that the dependencies that are needed for the task are not part of your main project any more.

- tests
- builds
- dev-dependencies like types as optional add able package via npx install-dev

that leads to cleaner repositorys with less direct dependencies. At present the most repos simply contain everything and strip everything on release
that scales not well the repos need to get structured in a modular way also else maintainance and upgrades are blocked and your not able to iterate
fast which is the most importent vital point to inovate a project. At Tesla for example Elon Musk has a single criteria that gets you fired and that is not
doing mistakes it is failing to inovate so if you want a job at Tesla you better follow that steps early to not get blocked later.

Your build steps and test steps are often always the same inside your indipendent packages thats why the people created MonoRepos to put the tooling for many packages into a central place. but that leads to less Modularity and big repos. 


