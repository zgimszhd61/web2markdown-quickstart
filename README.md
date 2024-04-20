# web2markdown-quickstart

```
import requests
from bs4 import BeautifulSoup

def html_to_markdown(url):
    try:
        response = requests.get(url)
        response.raise_for_status()  # 确保请求成功
        soup = BeautifulSoup(response.text, 'html.parser')

        markdown_content = ""

        # 抽取并转换标题
        if soup.title:
            markdown_content += f"# {soup.title.string}\n\n"

        # 抽取并转换段落
        for p in soup.find_all('p'):
            markdown_content += f"{p.get_text()}\n\n"

        # 如果需要抽取其他标签，可以在这里添加更多的处理逻辑
        # 例如抽取链接、图片等

        return markdown_content
    except requests.RequestException as e:
        return f"Error: {e}"

# 示例使用
url = "https://baoyu.io/translations/meta/meta-llama-3"  # 更换为你想要抽取的网址
markdown = html_to_markdown(url)
print(markdown)

```
