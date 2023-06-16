oc new-build ubi8/dotnet-60:latest~https://xy.git --name test-dot-net-build

oc tag --source=docker docker.artifactory.xy.cz/ubi8/dotnet-60:latest dot-net-build-image:latest

oc delete bc dot-net-test

oc delete is dot-net-build-image && oc delete bc dot-net-test && oc apply -f buildIS.yaml && oc apply -f bc.yaml && oc start-build dot-net-test --follow


oc cancel-build dot-net-test-1 && oc delete build dot-net-test-1

oc delete configmap s2i-assemble && oc create configmap s2i-assemble  --from-file=assemble
oc create configmap s2i-assemble2  --from-file=assemble2
oc delete builds $(oc get builds | grep 'Failed\|Complete' | awk '{print $1;}')

oc delete buildconfig $(oc get buildconfig |  awk '{print $1;}')

oc delete bc dot-net-test && oc delete is dot-net-build-image

oc delete is $(oc get is | grep 'release' | awk '{print $1;}')

oc create deployment dbidm-web-1 --image dbidm-web-builded:latest

oc get imagestreams -o json | ~/bin/jq.exe -r '.items[] | {imageStream:.metadata.name, image:.status.tags[]?.items[]?.image} | (.imageStream + "@" + .image)' | xargs -I {} ./cache-stdout oc get 'imagestreamimage/{}' -o json |  ~/bin/jq.exe -r '.image.dockerImageLayers[] | {name: .name, size: .size}' | ~/bin/jq.exe -sr 'unique_by(.name) | .[].size' | awk '{ sum += $1 } END { print (sum / 1024 / 1024 / 1024) "GB" }'

oc tag --source=docker docker.artifactory.xy.cz/xcy-web:feature-s2ibuild dbidm-web:feature-s2ibuild

oc create deployment dbidm-web-2 --image  docker.artifactory.xy.cz/rbcz/xy-web:feature-s2ibuild docker.artifactory.xy.cz/rbcz/xy:feature-s2ibuild
