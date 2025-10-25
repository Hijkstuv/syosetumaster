# syosetumaster
Simple crawling + translating project with syosetuka ni narou

install with :
```
pip install syosetumaster
```

recommanded import form :
```
from syosetumaster import SyosetuMaster as SM
```

You should set your openai API key :
```
SM.set_api_key("YOUR_API_KEY")
```

First, make SyosetuMaster instance :
```
master = SM()
```

You can create new Syosetu instance :
```
master.create_new_syosetu(
  syosetu_title = TITLE_OF_THE_SYOSETU    # not important. just for file I/O and classification
  syosetu_id = ID_OF_THE_SYOSETU      # e.g. n2267be -> read https://ncode.syosetu.com/n2267be/(episode_id) pages
  source_lang = "Japanese"       # trivialy, only "Japanese" works now... implemented for scalability
  target_lang = TARGET_LANGUAGE  # be careful: don't use language code, you should put whole language name e.g. EN(X) English(O)
)
```

or you can create new Syosetu instances :
```
master.create_new_syosetu_s(
  LIST_OF_ARGUMENTS  # : list[dict[str, str]]  e.g. [{"syosetu_title": "title_1", "syosetu_id": "id_1", ..}, ...]
)
```

These are automatically append to .syosetu_list :
```
master.syosetu_list    # -> list[Syosetu]
```

and you can save and load this list :
```
master.save_syosetu_list()
master.load_syosetu_list()
```
