# syosetumaster
Simple crawling + translating project with syosetuka ni narou

install with
```
pip install syosetumaster
```

recommanded import form is
```
from syosetumaster import SyosetuMaster as SM
```

You MUST set your openai API key.
```
SM.set_api_key("YOUR_API_KEY")
```

Files will be saved at "C:\\syosetu_task\\translate" and "C:\\syosetu_task\\batch".


make SyosetuMaster instance.
```
master = SM()
```

Create new Syosetu instance :
```
master.create_new_syosetu(
  syosetu_title = TITLE_OF_THE_SYOSETU    # not important. just for file I/O and classification
  syosetu_id = ID_OF_THE_SYOSETU      # e.g. "n2267be" -> read https://ncode.syosetu.com/n2267be/(episode_id) pages
  source_lang = "Japanese"       # trivialy, only "Japanese" works now... implemented for scalability
  target_lang = TARGET_LANGUAGE  # be careful: don't use language code, should be whole language name e.g. EN(X) English(O)
)
```

or Create new Syosetu instances :
```
master.create_new_syosetu_s(
  LIST_OF_KWARGS    # : list[dict[str, str]], e.g. [{"syosetu_title": "title_1", "syosetu_id": "id_1", ..}, ...]
)
```

created Syosetu instances are automatically append to .syosetu_list.
```
master.syosetu_list    # -> list[Syosetu]
```

save and load this list :
```
master.save_syosetu_list()
master.load_syosetu_list()
```

You can select novels that you want to treat.
```
master.select_syosetu(syosetu)
master.selected_syosetu_list = LIST_OF_SYOSETU    # this package is not completed, so this way would be more comfortable.
```

Crawl the syosetu :
```
master.crawl_syosetu(mode = "selected")
```
then all syosetu' in the master.selected_syosetu_list would be crawled.

-----------------------

Translate workflows contains 3+1 parts
- consistancy process
- glossary process
- translate process
- & post-translate process

```
master.consistancy_batches_request(mode = "selected")
master.consistancy_batches_response(mode = "selected")
master.glossary_batches_request(mode = "selected")
master.glossary_batches_response(mode = "selected")
master.translate_batches_request(mode = "selected")
master.translate_batches_response(mode = "selected")
master.post_translate_batches_request(mode = "selected")
master.post_translate_batches_response(mode = "selected")
```
note that response process takes long time. (each batch request takes 1\~5 minutes, and retrieving also takes 1\~2 seconds per batch)
if ~~~~_response task returns `False`, it means the task has not finished. You should rerun the task.
Don't worry - retrieved batches are already treated, so only newly completed batches will be retrieved while rerunning.
After all, you can export syosetu to txt file:
```
master.export_txt(mode = "selected")
```
