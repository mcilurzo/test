Feature Description

We want to implement the sbb-autocomplete.

https://lyne.sbb.ch/components/sbb-autocomplete

Figma Spec

References

https://angular.app.sbb.ch/angular/components/autocomplete/overview
https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/listbox_role
Design Spec

The autocomplete is an overlay attached to the respective input/sbb-form-field or a given origin
The autocomplete should wrap to an sbb-form-field if it is attached to an input inside an sbb-form-field (see shadow effect)
The width of the autocomplete is limited by the origin
Technical Spec

Note: Compare with sbb-menu and sbb-tooltip for certain behaviors

Important: Favorites (the star at the end of the options) are out of scope!
Delete the existing autocomplete components
Create sbb-option component (be aware that there will be a sbb-optgroup in the future, which can group options)
For keyboard interaction see https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/listbox_role#keyboard_interactions
Use HTML dialog element for options panel
Autocomplete should open below by default, but open above, if space below is not enough for the overlay
If both below and above do not have enough space, the overlay should be rendered on the side that has more space and allow scrolling
If the user scrolls the background and the available space changes, the overlay should adapt
The overlay should remain open on blur (closing conditions are Escape button, selecting an item via click or keyboard, a click or a focus outside of the autocomplete/input trigger)
Provide a possibility @Prop() origin: string | HTMLElement to define another origin (where the overlay is attached)
If the trigger is inside a sbb-form-field the autocomplete should automatically use the sbb-form-field as origin (if the origin is not manually defined)
Should implement the aria listbox pattern for the options: https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/listbox_role
sbb-option should have the possibility of defining/slotting an icon
sbb-autocomplete should have property @Prop() reserveIconSpace: boolean = false, which reserves space inside sbb-option for the icon, regardless if it is defined in the option or not (maybe use CSS variable)
Should support the sbb-divider with appropriate spacing
The text from the input should be highlighted (by not being bold) in the options, if available
Recommendation would be to hide the slot (but make it and only it screen reader accessible) and copy the slotted content to be displayed, while replacing all occurrences of the text with <span class="not-bold">text</span> and update this anytime either the slot content or the input text changes (maybe compare with https://github.com/sbb-design-systems/sbb-angular/blob/main/src/angular/core/option/option.ts#L266-L287 but it's a slightly different use case)
Should have a property @Prop() input: string | HTMLElement to connect an sbb-autocomplete to an input element
If sbb-autocomplete is placed inside an sbb-form-field it should automatically try to resolve the proper input element
If there are no options, do not show the panel
Provide events for sbb-autocomplete (e.g. will-open, did-open, will-close, did-close, selected, ...)
<sbb-form-field>
  <input>
  <sbb-autocomplete>
    <sbb-option>Value 1</sbb-option>
  </sbb-autocomplete>
</sbb-form-field>

<sbb-form-field>
  <input id="input1">
</sbb-form-field>
<sbb-autocomplete input="input1">
  <sbb-option>Value 1</sbb-option>
</sbb-autocomplete>
Definition of Done