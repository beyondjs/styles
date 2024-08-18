# `@beyond-js/styles`

This package provides tools for managing and processing styles within the BeyondJS framework, handling both legacy and
modern stylesheets. It integrates with other BeyondJS modules and supports features like dependency management and hot
module replacement (HMR).

## Features

-   **Style Registry**: Register and retrieve styles based on bundle identifiers.
-   **Legacy Style Support**: Compatibility with older BeyondJS applications.
-   **HMR for Styles**: Automatically updates styles in development environments without full page reloads.
-   **Dependency Management**: Recursively manages and applies styles for dependent bundles.

## Installation

```bash
npm install @beyond-js/styles
```

## Usage

### Registering Styles

Styles can be registered to the registry and later retrieved:

```typescript
import { styles } from '@beyond-js/styles';

// Register styles
styles.register('my-package/v1', '.my-class { color: red; }');

// Retrieve registered styles
const registeredStyle = styles.get('my-package/v1');
```

### Handling Legacy Styles

Legacy styles are processed and applied directly to the DOM:

```typescript
import LegacyStyles from '@beyond-js/styles/legacy';

const legacyStyles = new LegacyStyles('my-bundle', '.old-class { font-size: 12px; }');
legacyStyles.appendToDOM();
```

### Working with V1 Styles

V1 styles support versioning and are suitable for dynamic updates in a modern environment:

```typescript
import { V1Styles } from '@beyond-js/styles/v1';

const v1Style = new V1Styles('my-bundle');
console.log(v1Style.href); // Get the CSS URL with versioning
```

## API Overview

### Registry

-   `register(vspecifier: string, value: string): void`: Registers a style by its bundle specifier.
-   `get(vspecifier: string): LegacyStyles | V1Styles | undefined`: Retrieves registered styles.
-   `has(vspecifier: string): boolean`: Checks if styles are registered.

### LegacyStyles

-   `constructor(bundle: string, value: string)`: Initializes legacy styles.
-   `appendToDOM(is?: string): void`: Appends the stylesheet to the document head.

### V1Styles

-   `constructor(resource: string)`: Initializes styles for V1 bundles.
-   `get href(): string`: Returns the stylesheet URL with versioning.
-   `change(): void`: Triggers a version increment for HMR.

## License

This package is licensed under the MIT License.
