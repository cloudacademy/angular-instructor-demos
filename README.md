# To generate Docx or PDF from MD

## Pandoc Extension
- Make sure you have Pandoc extension installed in your VSCode
- Make sure you have Pandoc application installed in your machine 
    - you can install pandoc using Homebrew (macOS):

        ```
        brew install pandoc
        ```

- To generate docx or pdf
    - view > Command Pallete > Pandoc Render > select file format
    - Alternatively run following command from dir of your MD file

    ```
    pandoc README.md -o "Demo Guide.docx"
    ```
