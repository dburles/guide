# Blaze

1. Introduction to Blaze -- the tracker-backed handlebars like templating syntax
  1. Example of spacebars syntax, data context + helpers
  2. Hmmm. this is basically just the exact content of https://github.com/meteor/meteor/blob/devel/packages/spacebars/README.md#each I'm tempted to more or less just work through this verbatim for the first few sections. (sans the complicated stuff)
2. Creating reusable "pure" components with Blaze / best practice (a lot of this is repeating @sanjo's boilerplate)
  1. Validating data context fits a schema
  2. Always set data contexts to `{name: doc}` rather than just `doc`
  3. Use `{{#each .. in .. }}` to achieve the above
  4. Use the template instance as a component -- adding a `{{template}}` helper to access it
  5. Use a (named / scoped on _id if possible) reactive dict for instance state
  6. Attach functions to the template instance (in `onCreated`) to sensibly modify state
  7. Place `const template = Template.instance()` at the top of all helpers that care about state
  8. Always scope DOM lookups with `this.$`
  9. Use `.js-X` in event maps
  10. Pass extra content to components with `Template.contentBlock`, or named template arguments
  11. Use the `onRendered` callback to integrate w/ 3rd party libraries
3. Writing "smart" components with Blaze
  1. All of section 2.
  2. Use `this.autorun` and `this.subscribe`, listening to `FlowRouter` and `this.state`
  3. Set up cursors in helpers to be passed into pure sub-components, and filtered with `cursor-utils`
  4. Access stores directly from helpers.
4. Reusing code between templates
  1. Prefer utilities/composition to mixins or inheritance
  2. How to write global helpers
5. Understanding Blaze
  1. When does a template re-render (when its data context changes)
  2. When does a helper-rerun? (when its data context or reactive deps change)
    1. So be careful, this can happen a lot! If your helper is expensive, consider something like https://github.com/peerlibrary/meteor-computed-field
  3. How does an each tag re-run / decide when new data should appear?
  4. How do name lookups work?
  5. What does the build system do exactly?
  6. What is a view?
6. Testing Blaze templates
  1. Rendering a template in a unit test
  2. Querying the DOM (general but just a pointer here)
  3. Triggering reactivity and waiting for re-rendering
  4. Simulating events w/ JQ
7. Useful Blaze utilities / other approaches
  1. https://github.com/peerlibrary/meteor-blaze-components
  2. https://github.com/raix/Meteor-handlebar-helpers
  3. Much, much more...