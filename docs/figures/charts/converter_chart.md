## How to create OME-Zarr from my proprietary format?

- I perform an unary (one-to-one) conversion
  - I want to convert a single file
    - The file is small (fits in the memory)
      - I want a GUI
        - all OS -> Fiji 
        - Windows,macOS -> Fiji, NGFF-Converter
      - Command line -> bioformats2raw
    - The file is large
      - I want a GUI
        - Windows,macOS -> NGFF-Converter
      - I want a command line tool        
        - all OS -> bioformats2raw
  - I want to perform a batch conversion
    - I want a GUI
      - Windows,macOS -> NGFF-Converter
    - I want a command line tool
      - Linux,macOS -> BatchConvert, EuBI-Bridge
      - all OS -> EuBI-Bridge
- I want to perform an aggregative conversion (multiple input files to one OME-Zarr)
  - I want to convert an HCS dataset
    - I have a companion-ome file
      - I want a GUI
        - Windows,macOS -> NGFF-Converter
      - I want a command line tool
        - All OS -> bioformats2raw
    - I don't have a companion-ome file
      - You need to create one! 
  - I want to convert a multi-file series (multiple time points, channels, z slices, etc., in diffferent files)
    - I have a companion-ome file
      - I want a GUI
        - Windows,macOS -> NGFF-Converter
      - I want a command line tool
        - All OS -> bioformats2raw
    - I don't have a companion-ome file (but file names are informative)
      - All OS -> EuBI-Bridge 



```mermaid
{
  "name": "Conversion Decision Tree",
  "children": [
    {
      "name": "Unary (one-to-one) conversion",
      "children": [
        {
          "name": "Single file",
          "children": [
            {
              "name": "Small file (fits in memory)",
              "children": [
                {
                  "name": "GUI",
                  "children": [
                    { "name": "All OS -> Fiji" },
                    { "name": "Windows, macOS -> Fiji, NGFF-Converter" }
                  ]
                },
                { "name": "Command line -> bioformats2raw" }
              ]
            },
            {
              "name": "Large file",
              "children": [
                {
                  "name": "GUI",
                  "children": [
                    { "name": "Windows, macOS -> NGFF-Converter" }
                  ]
                },
                {
                  "name": "Command line",
                  "children": [
                    { "name": "All OS -> bioformats2raw" }
                  ]
                }
              ]
            }
          ]
        },
        {
          "name": "Batch conversion",
          "children": [
            {
              "name": "GUI",
              "children": [
                { "name": "Windows, macOS -> NGFF-Converter" }
              ]
            },
            {
              "name": "Command line",
              "children": [
                { "name": "Linux, macOS -> BatchConvert, EuBI-Bridge" },
                { "name": "All OS -> EuBI-Bridge" }
              ]
            }
          ]
        }
      ]
    },
    {
      "name": "Aggregative conversion (multiple input files to one OME-Zarr)",
      "children": [
        {
          "name": "HCS dataset",
          "children": [
            {
              "name": "Companion-OME file",
              "children": [
                {
                  "name": "GUI",
                  "children": [
                    { "name": "Windows, macOS -> NGFF-Converter" }
                  ]
                },
                {
                  "name": "Command line",
                  "children": [
                    { "name": "All OS -> bioformats2raw" }
                  ]
                }
              ]
            },
            { "name": "No companion-OME file -> You need to create one!" }
          ]
        },
        {
          "name": "Multi-file series",
          "children": [
            {
              "name": "Companion-OME file",
              "children": [
                {
                  "name": "GUI",
                  "children": [
                    { "name": "Windows, macOS -> NGFF-Converter" }
                  ]
                },
                {
                  "name": "Command line",
                  "children": [
                    { "name": "All OS -> bioformats2raw" }
                  ]
                }
              ]
            },
            {
              "name": "No companion-OME file (but filenames are informative)",
              "children": [
                { "name": "All OS -> EuBI-Bridge" }
              ]
            }
          ]
        }
      ]
    }
  ]
}

```