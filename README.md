# Rise Page Web Component

## Introduction
`rise-page` is a web component that controls the playback of its child components, telling them when to play, pause or stop. Additionally, it surfaces methods for returning details about the Display.

`rise-page` works in conjunction with [Rise Vision](http://www.risevision.com), the [digital signage management application](http://rva.risevision.com/) that runs on [Google Cloud](https://cloud.google.com).

At this time Chrome is the only browser that this project and Rise Vision supports.

## Usage
To begin, you will need to install `rise-page` using Bower:
```
bower install https://github.com/Rise-Vision/web-component-rise-page.git
```

Next, construct your HTML page. You should include `webcomponents-lite.min.js` before any code that touches the DOM, and load the web component using an HTML import. For example:
```
<!DOCTYPE html>
<html>
  <head>
    <script src="bower_components/webcomponentsjs/webcomponents-lite.min.js"></script>
    <link rel="import" href="bower_components/web-component-rise-page/rise-page.html">
  </head>
  <body>
    <!-- Replace "dummy-id" with a valid Display ID. -->
    <rise-page id="page" display-id="dummy-id">
      <!-- Child components go here. -->
    </rise-page>
  </body>
</html>
```

### Attributes
| Attribute               | Type                              | Default |
| ----------------------- | --------------------------------- | :-----: |
| `display-id` (required) | `<string>` The ID of the Display. | `''`    |

*Note:* You can find the Display ID on the Displays page of the [Rise Vision platform](http://rva.risevision.com/).

### Child Components
Child components can themselves be web components. Regardless of the form that they take, they need to adhere to some rules in order for the page component to be able to control their playback.

#### rise-component-ready
Once a component has finished initializing and loading, it should dispatch the `rise-component-ready` event, passing custom data that includes the functions that the page component should call to control its playback, if applicable, and whether or not it supports sending the `rise-component-done` event. For example:
```
var readyEvent = new CustomEvent("rise-component-ready", {
  "detail": {
    "play": playFunction,
    "pause": pauseFunction,
    "stop": stopFunction,
    "done": true
  },
  "bubbles": true
});

elem.dispatchEvent(readyEvent);
```

#### rise-component-done
When a component that supports the `rise-component-done` event has completed a single playback cycle, it should dispatch that event. For example:
```
this.dispatchEvent(new CustomEvent("rise-component-done", { "bubbles": true }));
```

A sample child component that is built as a web component can be seen [here](https://github.com/Rise-Vision/web-component-rise-page/blob/master/rise-demo.html). You will need to replace the `display-id` attribute of the `<rise-page>` element with a valid Display ID in order to return data.

### Methods
| Method              | Description                                                         |
| ------------------- | ------------------------------------------------------------------- |
| `getDisplayId`      | Returns the Display ID.                                             |
| `getCompanyId`      | Returns the Company ID of the Display.                              |
| `getDisplayAddress` | Returns the Display address.                                        |

## Built With
- [Polymer](https://www.polymer-project.org/)
- [webcomponentsjs](https://github.com/webcomponents/webcomponentsjs)
- [Polymer iron-ajax](https://elements.polymer-project.org/elements/iron-ajax)
- [npm](https://www.npmjs.org)
- [Bower](http://bower.io/)
- [Gulp](http://gulpjs.com/)
- [Polyserve](https://www.npmjs.com/package/polyserve)
- [web-component-tester](https://github.com/Polymer/web-component-tester) for testing

## Development

### Dependencies
* [Git](http://git-scm.com/) - Git is a free and open source distributed version control system that is used to manage our source code on Github.
* [npm](https://www.npmjs.org/) & [Node.js](http://nodejs.org/) - npm is the default package manager for Node.js. npm runs through the command line and manages dependencies for an application. These dependencies are listed in the _package.json_ file.
* [Bower](http://bower.io/) - Bower is a package manager for Javascript libraries and frameworks. All third-party Javascript dependencies are listed in the _bower.json_ file.
* [Gulp](http://gulpjs.com/) - Gulp is a Javascript task runner. It lints, runs unit and E2E (end-to-end) tests, minimizes files, etc. Gulp tasks are defined in _gulpfile.js_.
* [Polyserve](https://www.npmjs.com/package/polyserve) - A simple web server for using bower components locally.

### Local Development Environment Setup and Installation
To make changes to the web component, you'll first need to install the dependencies:

- [Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Node.js and npm](http://blog.nodeknockout.com/post/65463770933/how-to-install-node-js-and-npm)
- [Bower](http://bower.io/#install-bower) - To install Bower, run the following command in Terminal: `npm install -g bower`. Should you encounter any errors, try running the following command instead: `sudo npm install -g bower`.
- [Gulp](https://github.com/gulpjs/gulp/blob/master/docs/getting-started.md) - To install Gulp, run the following command in Terminal: `npm install -g gulp`. Should you encounter any errors, try running the following command instead: `sudo npm install -g gulp`.
- [Polyserve](https://www.npmjs.com/package/polyserve) - To install Polyserve, run the following command in Terminal: `npm install -g polyserve`. Should you encounter any errors, try running the following command instead: `sudo npm install -g polyserve`.

The web component can now be installed by executing the following commands in Terminal:
```
git clone https://github.com/Rise-Vision/web-component-rise-page.git
cd web-component-rise-page
npm install
bower install
```

### Run Locally
To access the demo locally, run the `polyserve` command in Terminal.

In your browser, navigate to:
```
localhost:8080/components/rise-page/demo.html
```

### Testing
You can run the suite of tests from the command line or via a local web server using Polyserve.

#### Command Line
Execute the following command in Terminal to run the tests:
```
gulp test
```

#### Local Server
Run the `polyserve` command in Terminal.

In your browser, navigate to:
```
localhost:8080/components/rise-page/test/
```

### Deployment
Once you are satisifed with your changes, deploy `rise-page.html`, as well as the `bower_components/iron-ajax`, `bower_components/polymer`, and `bower_components/webcomponentsjs` folders to your server. You can then use the web component by following the *Usage* instructions above.

## Submitting Issues
If you encounter problems or find defects we really want to hear about them. If you could take the time to add them as issues to this Repository it would be most appreciated. When reporting issues, please use the following format where applicable:

**Reproduction Steps**

1. did this
2. then that
3. followed by this (screenshots / video captures always help)

**Expected Results**

What you expected to happen.

**Actual Results**

What actually happened. (screenshots / video captures always help)

## Contributing
All contributions are greatly appreciated and welcome! If you would first like to sound out your contribution ideas, please post your thoughts to our [community](http://community.risevision.com), otherwise submit a pull request and we will do our best to incorporate it. Please be sure to submit test cases with your code changes where appropriate.

## Resources
If you have any questions or problems, please don't hesitate to join our lively and responsive community at http://community.risevision.com.

If you are looking for user documentation on Rise Vision, please see http://www.risevision.com/help/users/

If you would like more information on developing applications for Rise Vision, please visit http://www.risevision.com/help/developers/.

**Facilitator**

[Donna Peplinskie](https://github.com/donnapep "Donna Peplinskie")
