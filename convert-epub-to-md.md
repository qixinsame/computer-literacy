# 1. Create the Quick Actions

这一步的目的是建立一个快捷操作，当我们在Mac上右键点击epub文件的时候，在`Quick Actions`下面会出现`Convert EPUB to Markdown`的选项。

![Screenshot 2025-01-04 at 10.30.24](/Users/qixin/Student/computer-literacy/images/quickaction.png)

**方法1:**

直接访问这个repo里面的文章 [NotebookLM](https://github.com/xiaolai/apple-computer-literacy/blob/main/NotebookLM.md) ,通过编辑Shell脚本还实现这个功能。

**方法2:**

上述文章里还提供了一个workflow的文件，直接下载这个workflow文件：[Convert EPUB to Markdown Workflow](https://raw.githubusercontent.com/xiaolai/apple-computer-literacy/main/files/Convert%20EPUB%20to%20Markdown.zip) 然后将其保存到`~/Library/Services`就可以了。



# 2. 调整：用Python脚本将`html`转换成`markdown`格式



目前（2025/01/04）还不知道是什么原因，利用上述方法只能将`epub`文件转化成一份全文的`txt` 文件和所有章节的 `html`文件。目前还不能将章节`html`文件直接转化成`Markdown`文件。所以在ChatGPT的帮助下（[Chat Hisotry](https://chatgpt.com/c/677739ce-6d98-8012-80d5-2e7a9e7a886b))，我用下面的Python脚本完成了最后的一步“

1. Install Pandoc

   ```bash
   brew install pandoc
   ```

2. Install Markdownify

   ```bash
   pip install markdownify
   ```

3. Run below Python script to convert multiple HTML files to Markdown

   ```python
   import os
   from markdownify import markdownify as md
   
   def convert_html_to_markdown(input_dir, output_dir):
       """
       Converts all HTML files in the input directory to Markdown files in the output directory.
   
       Args:
           input_dir (str): Path to the directory containing HTML files.
           output_dir (str): Path to the directory to save Markdown files.
       """
       # Ensure the output directory exists
       os.makedirs(output_dir, exist_ok=True)
   
       # Loop through all files in the input directory
       for filename in os.listdir(input_dir):
           if filename.endswith(".html"):  # Process only HTML files
               input_path = os.path.join(input_dir, filename)
               output_path = os.path.join(output_dir, os.path.splitext(filename)[0] + ".md")
   
               # Read the HTML file
               with open(input_path, "r", encoding="utf-8") as html_file:
                   html_content = html_file.read()
   
               # Convert to Markdown
               markdown_content = md(html_content)
   
               # Write the Markdown content to a new file
               with open(output_path, "w", encoding="utf-8") as md_file:
                   md_file.write(markdown_content)
               
               print(f"Converted: {input_path} -> {output_path}")
   
   # Define input and output directories
   input_directory = "path/to/html/files"
   output_directory = "path/to/output/markdown/files"
   
   # Run the conversion
   convert_html_to_markdown(input_directory, output_directory)
   
   ```

   Replace `path/to/html/files` and `path/to/output/markdown/files` with the paths to your HTML files and the directory where you want to save the Markdown files.