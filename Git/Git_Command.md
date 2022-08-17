# Git Command

[Git - git-mv Documentation](https://www.git-scm.com/docs/git-mv)

![바이너리 값이 바뀜](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/24c4feef-675f-4847-9a9b-79c54bd7ebb8/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220817%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220817T052847Z&X-Amz-Expires=86400&X-Amz-Signature=a4fa6ea5055452894e024b6a36ee9638f97b0336cfaac2de6b992e2340222c7e&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

바이너리 값이 바뀜

![git mv는 renamed 사실을 명확히 알려준다. 바이너리 값이 바뀌지 않았으므로 git add가 불필요하다.](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/efbbc58c-843f-4fab-84a9-0d3a93368d56/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220817%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220817T052912Z&X-Amz-Expires=86400&X-Amz-Signature=16ddb9b0adee6dac8fbe2a1d625a0a4fe21ff4d3b1c74af9378a2623ff899e35&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

git mv는 renamed 사실을 명확히 알려준다. 바이너리 값이 바뀌지 않았으므로 git add가 불필요하다.

![이런 것도 git mv를 써주자](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/b016e29b-4727-4f02-b26f-b6ca4c72eeb4/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220817%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220817T052934Z&X-Amz-Expires=86400&X-Amz-Signature=29c3cb9db600ad8289a163cb8d0c385439b6a6ad513f332541e3a838f6ea671f&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

이런 것도 git mv를 써주자

git checkout → git restore, git switch

![Untitled](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/da0d84fd-4680-461d-b153-825283e44af6/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220817%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220817T052951Z&X-Amz-Expires=86400&X-Amz-Signature=f4188d0b02b5753c13316e373839f40becccae59cd7234aeae6eef4031c4fece&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

merge : 나대로 진행하다가 마지막에 병합할 때 conflict를 해결하고 merge하겠다.

rebase : 변화가 있을 때마다 내 branch를 refresh하면서 conflict를 해결하고 merge하겠다.

![커밋 메시지 수정하기](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/4ee14b58-3adb-440b-a7df-993be939359d/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220817%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220817T053004Z&X-Amz-Expires=86400&X-Amz-Signature=b561fdc7b9c490d897d384efd01cafa3c5a6528c2396fd8f3a178186668d8b2b&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

커밋 메시지 수정하기

![revert](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/68b291f5-6b00-4271-a16d-3ef1ee76e501/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220817%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220817T053018Z&X-Amz-Expires=86400&X-Amz-Signature=17fea5e5a001626d17179253634b08627f5776031ac9031edc68ed731037c6c8&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

revert

merge commit을 되돌릴 땐

-m

git revert -m {1 or 2} {merge commit id}
