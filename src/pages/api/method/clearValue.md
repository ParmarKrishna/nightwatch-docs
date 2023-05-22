### Examples

The example below navigates to google.com, searches for the term "nightwatch.js", then clears the input using _clearValue_ command and finally verifies if the results container is empty:

```js

module.exports = {
  before : function(browser) {
    // see <https://github.com/nightwatchjs/nightwatch/blob/main/examples/globalsModule.js#L12>
    browser.globals.waitForConditionTimeout = 5000;
  },

  'clearValue example test' : function (browser) {

    browser
      .url('https://google.com')
      .waitForElementVisible('input[type=text]')
      .setValue('input[type=text]', 'nightwatch.js')
      .click('button[type=submit]')
      .expect.element('#rcnt').text.to.contain('nightwatchjs.org/');

    browser
      .clearValue('input[type=text]')
      .expect.element('#rcnt').text.to.equal('');
  },

  after : function(browser) {
    browser.end();
  }
};

```

### Output

```bash
[Clear Value] Test Suite
============================

Running:  clearValue example test
 ✔ Element <input[type=text]> was visible after 68 milliseconds.
 ✔ Expected element <#rcnt> text to contain: "nightwatchjs.org/" - condition was met in 763ms
 ✔ Expected element <#rcnt> text to equal: "" - condition was met in 36ms

OK. 3 assertions passed. (7.593s)
```

### Possible Errors

Here are the type of errors that you might get when using `clearValue`. Full error details are available when running nightwatch with `--verbose` flag.

- ```invalid element state``` - if the referenced element is disabled or is not displayed.
- ```element not visible``` - if the referenced element is not visible on the page (either is hidden by CSS, has 0-width, or has 0-height)
