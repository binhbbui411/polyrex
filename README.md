# \<polyrex-store\>

Vuex like bindings for polymer

Usage:
```html
<dom-module id="polyrex-sample">
  <template>
    <polyrex-store
      state="[[initialState]]"
      mutations="[[mutations]]"
      actions="[[actions]]"
    ></polyrex-store>

    <div>
      <div>Value: [[val]]</div>
      <input on-input="updateInput" value="[[val]]" />
    </div>
  </template>
  <script>
    class PolyrexSample extends PolyRex(Polymer.Element) {
      static get is() { return 'polyrex-sample'; }
      constructor() {
        super();

        this.initialState = {
          hello: 'World',
          fields: {}
        };
        this.mutations = {
          'UPDATE_INPUT'(state, payload) {
            state.fields.input = payload.value;
          },
          'BUTTON_CLICK'(state, payload) {
            state.clicked = payload.clicked;
          }
        };
        this.actions = {
          'BUTTON_CLICK'({ commit }, payload) {
            commit('BUTTON_CLICK', payload);
          },
          'UPDATE_INPUT'({ commit }, payload) {
            commit('UPDATE_INPUT', payload)
          }
        };
      }

      _computed() {
        return this.mapState({
          val: state => state.fields.input
        });
      }

      updateInput(e) {
        this.dispatch('UPDATE_INPUT', { value: e.target.value });
      }
    }

    window.customElements.define(PolyrexSample.is, PolyrexSample);
  </script>
</dom-module>
```

Start by using the PolyRex mixin `class MyComponent extends PolyRex(Polymer.Element)`

Then you have access to functions like dispatch, mapState, and _computed. map state is an object whose keys are turned into properties based on the callback.
dispatch is used to trigger updates to state.

The usual flow goes something like this:
initial state -> dispatch action -> commit -> mutation -> re render

## Install the Polymer-CLI

First, make sure you have the [Polymer CLI](https://www.npmjs.com/package/polymer-cli) installed. Then run `polymer serve` to serve your element locally.

## Viewing Your Element

```
$ polymer serve
```

## Running Tests

```
$ polymer test
```

Your application is already set up to be tested via [web-component-tester](https://github.com/Polymer/web-component-tester). Run `polymer test` to run your application's test suite locally.
