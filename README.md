#📜 Project Setup

This project uses 📦️ pnpm, but any package manager will work.

1. Clone the Project
Clone the repository from GitHub:

sh
Copy code
git clone https://github.com/adebare-adeyemo/Editor-.git
2. Navigate to the Project Directory
Change into the project directory:

sh
Copy code
cd editor
3. Install Dependencies
Install the project dependencies using pnpm. If you don’t have pnpm installed, you can install it globally using npm:

sh
Copy code
npm install -g pnpm
Then, install the dependencies:

sh
Copy code
pnpm install
4. Run the Development Server
Start the development server:

sh
Copy code
pnpm run dev
Alternatively, you can build and preview the project:

sh
Copy code
pnpm run build && pnpm run preview
Additional Debugging and Fixes
If you encounter the Cannot read properties of undefined (reading 'core') error, follow these steps to debug and fix the issue:

Check for Proper Initialization in posts.ts
Ensure all necessary modules are correctly imported and initialized in src/lib/posts.ts. For example:

typescript
Copy code
// src/lib/posts.ts

import { getRateLimit } from 'some-library';

function getRateLimitInfo() {
  const someObject = getSomeObject(); // Ensure this returns a defined object
  if (!someObject || !someObject.core) {
    throw new Error('someObject or someObject.core is undefined');
  }
  return someObject.core.getRateLimit();
}

try {
  const rateLimit = getRateLimitInfo();
  console.log('Rate Limit:', rateLimit);
} catch (error) {
  console.error('Error getting rate limit:', error);
}
Verify Environment Variables
Ensure the environment variables are set up correctly in a .env file in the root directory:

plaintext
Copy code
VITE_SUPABASE_URL=https://your-supabase-url.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-key
Verify Supabase Client Initialization
Ensure the Supabase client is initialized correctly in supabase.ts:

typescript
Copy code
import { createClient } from '@supabase/supabase-js';

const supabaseUrl = import.meta.env.VITE_SUPABASE_URL;
const supabaseAnonKey = import.meta.env.VITE_SUPABASE_ANON_KEY;

if (!supabaseUrl || !supabaseAnonKey) {
  throw new Error('supabaseUrl and supabaseAnonKey are required.');
}

export const supabase = createClient(supabaseUrl, supabaseAnonKey);
Verify Vite Configuration
Ensure Vite is configured to load the environment variables correctly. Your vite.config.js should look like this:

javascript
Copy code
import { defineConfig } from 'vite';
import svelte from '@sveltejs/vite-plugin-svelte';
import dotenv from 'dotenv';

dotenv.config();

export default defineConfig({
  plugins: [svelte()],
});
Restart the Development Server
After making any changes, restart your development server:

sh
Copy code
pnpm run dev
By following these steps, you should be able to set up, run, and debug your project effectively. If you encounter any specific issues or errors, provide additional details for more targeted assistance.
