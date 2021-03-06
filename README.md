grunt-typescript
================

## Changes from master branch
This branch has been developed for better watching and compiling of typescript files.

    1. Removed resolving of "path" in "watch to Enable chokidar multiple file watching
    2. Added updateFileSnapshot method to update a cached files contents

[![Build Status](https://travis-ci.org/k-maru/grunt-typescript.png?branch=master)](https://travis-ci.org/k-maru/grunt-typescript) [![NPM version](https://badge.fury.io/js/grunt-typescript.png)](http://badge.fury.io/js/grunt-typescript)

[![NPM](https://nodei.co/npm/grunt-typescript.png?downloads=true)](https://nodei.co/npm/grunt-typescript/)

Compile TypeScript in Grunt

[Release Note](CHANGELOG.md)

## Documentation
You'll need to install `grunt-typescript` first:

    npm install grunt-typescript --save-dev

or add the following line to devDependencies in your package.json

    "grunt-typescript": "",

Then modify your `Gruntfile.js` file by adding the following line:

    grunt.loadNpmTasks('grunt-typescript');

Then add some configuration for the plugin like so:

    grunt.initConfig({
        ...
        typescript: {
          base: {
            src: ['path/to/typescript/files/**/*.ts'],
            dest: 'where/you/want/your/js/files',
            options: {
              module: 'amd', //or commonjs
              target: 'es5', //or es3
              basePath: 'path/to/typescript/files',
              sourceMap: true,
              declaration: true
            }
          }
        },
        ...
    });
   
If you want to create a js file that is a concatenation of all the ts file (like -out option from tsc), 
you should specify the name of the file with the '.js' extension to dest option.

    grunt.initConfig({
        ...
        typescript: {
          base: {
            src: ['path/to/typescript/files/**/*.ts'],
            dest: 'where/you/want/your/js/file.js',
            options: {
              module: 'amd', //or commonjs
            }
          }
        },
        ...
    });

##Options

###noLib `boolean`
Do not include a default lib.d.ts with global declarations

###target `string`
Specify ECMAScript target version: "ES3" (default) or "ES5"

###module `string`
Specify module code generation: "commonjs" (default) or "amd"

###sourceMap `boolean`
Generates corresponding .map files

###declaration `boolean`
Generates corresponding .d.ts file

###comments `boolean`
Emit comments to output

###noImplicitAny `boolean`
Warn on expressions and declarations with an implied 'any' type.

###noResolve `boolean`
Skip resolution and preprocessing.

##Original Options

###newLine `string`
Specify newline code: "auto" (default) or "crlf" or "lf". This options is experimental.

###indentStep `number`
Specify space indent count for code generation: This value will be disregarded if the useTabIndent option is specified. This options is experimental.

###useTabIndent `boolean`
Specify tab indent for code generation: false (default) or true. This options is experimental.

###ignoreError `boolean`
If the compiler can create a file, the task ignores the error.
Default value is false.

###disallowAsi `boolean`
Do not allow auto semicolon insertion. This options is experimental.

###basePath `string`
Path component to cut off when mapping the source files to dest files.

###watch `string` or `boolean` or `object`
Watch .ts files.
It runs very quickly the second time since the compilation. It is because you only want to read and output file is limited.

Specify the directory where you want to monitor in the options.

    grunt.initConfig({
            ...
        typescript: {
          base: {
            src: ['path/to/typescript/files/**/*.ts'],
            options: {
              watch: 'path/to/typescript/files'
            }
          }
        },
        ...
    });

If you specify the true, then automatically detects the directory.

    grunt.initConfig({
            ...
        typescript: {
          base: {
            src: ['path/to/typescript/files/**/*.ts'],
            options: {
              watch: true   //Detect all target files root. eg: 'path/to/typescript/files/'
            }
          }
        },
        ...
    });

For expansion of the future, You can also be specified 'object'.

    grunt.initConfig({
            ...
        typescript: {
          base: {
            src: ['path/to/typescript/files/**/*.ts'],
            options: {
              watch: {
                path: ['path/to/typescript/files/**/*.ts'], // You can now use arrays of ts files or folders
                before: ['beforetasks'],   //Set before tasks. eg: clean task
                after: ['aftertasks']      //Set after tasks.  eg: minify task
                atBegin: true              //Run tasks when watcher starts. default false
              }
            }
          }
        },
        ...
    });

※I'm sorry for poor English
