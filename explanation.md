# Prompts-JS Library Guide

## Overview

Prompts-JS is a lightweight, dependency-free JavaScript library that provides modern alternatives to traditional browser dialog boxes. It implements an async promise-based approach to replace the standard `alert()`, `confirm()`, and `prompt()` functions.

## Key Features

- Async/Promise-based implementation
- Lightweight with no dependencies
- Accessible for screen readers
- Customizable styling options
- Non-blocking user interface

## Core Concepts

### Traditional vs Modern Approach

#### Traditional Browser Dialogs

```javascript
// Alert - blocks everything until user clicks OK
alert("Your file was saved!");

// Confirm - blocks everything until user picks Yes/No
if (confirm("Delete this file?")) {
    deleteFile();
}

// Prompt - blocks everything until user types something
const name = prompt("What's your name?");
```

#### Modern Prompts-JS Approach

```javascript
// Alert - doesn't block other code from running
await Prompts.alert("Your file was saved!");

// Confirm - more flexible and non-blocking
const userWantsToDelete = await Prompts.confirm("Delete this file?");
if (userWantsToDelete) {
    deleteFile();
}

// Prompt - can be styled and is more accessible
const name = await Prompts.prompt("What's your name?");
```

## Common Usage Patterns

### Basic Usage Example

```javascript
// Alert
await Prompts.alert("This is an alert message!");
console.log("Alert closed");

// Confirm
const confirmed = await Prompts.confirm("Are you sure you want to proceed?");
if (confirmed) {
    console.log("User confirmed");
} else {
    console.log("User canceled");
}

// Prompt for a string
const userInput = await Prompts.prompt("Please enter your name:");
if (userInput) {
    console.log("User entered:", userInput);
} else {
    console.log("User canceled or entered nothing");
}
```

### Advanced Usage Examples

#### Error Handling with Try/Catch

```javascript
try {
    const name = await Prompts.prompt("Enter your name:");
    const age = await Prompts.prompt("Enter your age:");

    if (name && age) {
        await Prompts.alert(`Hello ${name}, you are ${age} years old!`);
    }
} catch (error) {
    console.error("Something went wrong:", error);
}
```

#### Form Validation Example

```javascript
const saveChanges = async () => {
    const hasUnsavedChanges = true; // example condition

    if (hasUnsavedChanges) {
        const shouldProceed = await Prompts.confirm("You have unsaved changes. Continue anyway?");
        if (!shouldProceed) {
            return false;
        }
    }

    // proceed with navigation/action
    return true;
};
```

## Benefits

1. **Improved User Experience**
   - Application remains responsive while dialogs are open
   - No page blocking during user interaction
   - Smoother integration with modern web applications

2. **Developer Benefits**
   - Clean, promise-based API
   - Easy to integrate with async/await syntax
   - Flexible error handling
   - Consistent behavior across browsers

3. **Accessibility**
   - Better screen reader support
   - Improved keyboard navigation
   - ARIA compliance

4. **Customization**
   - Styleable to match application design
   - Configurable behavior
   - Extensible functionality

## Best Practices

1. Always use `await` when calling Prompts-JS methods
2. Implement proper error handling using try/catch
3. Consider user experience when chaining multiple dialogs
4. Provide clear, concise messages in dialog content
5. Test accessibility with screen readers
6. Ensure proper keyboard navigation support
