# FMRI PROJECT (YALE Dataset)

The image data is acquired from [this](https://fcon_1000.projects.nitrc.org/indi/cmi_healthy_brain_network/sharing_neuro.html) repository.

```javascript
const checkboxes = document.querySelectorAll('input[type="checkbox"]');
let urls = [];
checkboxes.forEach((checkbox) => {
    urls.push(checkbox.value);
});

copy(urls);
```

For each release, copy the above piece of JS code in your browser console. This
will directly copy all the links to the images to your clipboard. Then simply
output the contents of your clipboard in a text file. 
Now, suppose you have a list of participants you want to work with, use `grep`
to extract the URLs from this file now and `wget` to directly download the
tarballs locally.

```bash
# fetch_data.sh
rm -f not_found.txt

SUBEJCT_LIST=(
    NDARUD306BB0
    NDARPF179GNV
    NDARPF395NV5
    NDARXV034WE0
    NDARRC190NKB
)

for sub in "${SUBJECT_LIST[@]}"; do
    url=$(grep ${sub} ./all_participant_urls.txt)
    if [ -z "${url}" ]; then 
        echo $sub >> not_found.txt
    else
        # Download the tarball using `wget`.
        wget -c ${url//\"/}
    fi
done
```

