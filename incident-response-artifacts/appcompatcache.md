# AppCompatCache

## Overview
* Created by Microsoft to identify application compatibility issues, helps developers troubleshoot legacy functions
  * Windows looks at AppCompatCache to determine if modules require shimming for compatibility
  * The Cache data tracks file path, size, last modified time, and last execution time (depending on OS)
* Most recent on top, written on shutdown
