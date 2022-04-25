## SurveyBank

For SurvayBank meta data access: https://www.dropbox.com/sh/tcn5e8trysnplio/AACE7uutKT9eQFmrRE8xL1hma?dl=0

## Data format

Each sample contains three parts, including:

1. meta information
2. body text (`body_text`)
3. biblography entries (`bib_entries`)

For those keys that are mentioned here, most of them are aligned with S2ORC. You can refer to [link](https://github.com/allenai/s2orc) for more details.

### Meta information

The first part of the sample includes several crucial keys for identification such as `title`. To align SurveyBank with S2ORC, we also assign `paper_id` to each paper
whenever possible, referring to the corresponding paper entity in S2ORC. `unique_id` is generated automatically for each sample in the dataset, to uniquely identify every paper within SurveyBank. Keys like `title`, `authors`, `year`, `venue`, `abstract`, `publisher`, `keywords`, `language` store information extracted from the paper by Grobid; among these, `authors` will be placed with an empty list object if the corresponding information is missing; the rest keys will be placed with `None` if the information is missing. All samples are categorized into three types: *regular*, *roman_alphabet*, and *other*, indicated by key `paper_type`. *regular* means that the paper has section titles prefixed with numbers and the ratio of valid section titles is bigger than 0.65. *roman_alphabet* means the paper can be detected with roman section titles and the ratio of valid section title (after the roman alphabet section titles are transformed into regular type) is bigger than 0.8. The rest are classified as *other*. An example of meta information is shown below.

```
{
    "title": "A Survey on Hate Speech Detection using Natural Language Processing",
    "paper_id": "9626793",
    "_pdf_hash": null,
    "authors": [
        {
            "first": "Anna",
            "middle": [],
            "last": "Schmidt",
            "suffix": ""
        },
        {
            "first": "Michael",
            "middle": [],
            "last": "Wiegand",
            "suffix": ""
        }
    ],
    "year": "2017",
    "venue": "Proceedings of the Fifth International Workshop on Natural Language Processing for Social Media",
    "abstract": "This paper presents a survey on hate speech detection",
    "unique_id": "8YY3MFr",
    "publisher": "Association for Computational Linguistics",
    "abbr_authors": [
        "Anna Schmidt",
        "Michael Wiegand"
    ],
    "keywords": null,
    "paper_type": "regular",
    "language": "en",
    "pdf_link": "https://www.aclweb.org/anthology/W17-1101.pdf",
    "cited_by": 343,
    ...
}
```

### Body text

The `body_text` includes main body of the paper and references mentioned. `n` denotes the hierarchical structure level of its corresponding section in the paper; for example, `n` with value 1.2 indicates the corresponding section being the second subsection of the first section. An example of body text is shown below.

```
{
    "body_text": [
        {
            "section": "Introduction",
            "n": "1",
            "paragraphs": [
                {
                    "text": "Hate speech is commonly...",
                    "cite_spans": [
                        {
                            "start": 232,
                            "end": 248,
                            "text": "(Nockleby, 2000)",
                            "ref_id": "BIBREF21"
                        },
                        ...
                    ],
                    "ref_spans": []
                },
                ...
            ]
        },
        {
            "section": "Terminology",
            "n": "2",
            "paragraphs": [
                {
                    "text": "In this paper we...",
                    "cite_spans": [],
                    "ref_spans": []
                },
                ...
            ]
        },
        ...
    ]
}
```
### Biblography entries

Here `link` denotes its corresponding entity id (`paper_id`) within S2ORC after alignment. Note that the key in `bib_entries` correspond to the `ref_id` with in `body_text`. An example is shown below.

```
{
    "bib_entries": {
        "BIBREF0": {
            "title": "Latent Dirichlet Allocation",
            "authors": [
                {
                    "first": "David",
                    "middle": [
                        "M"
                    ],
                    "last": "Blei",
                    "suffix": ""
                },
                ...
            ],
            "year": "2003",
            "venue": "Journal of Machine Learning Research",
            "link": "3177797",
            "publisher": null,
            "unique_id": "9oQvQm8"
        },
        ...
    }
}
```
