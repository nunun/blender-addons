# blender-addons

* install location
  * 2.75
    * Win: C:\Users\<username>\AppData\Roaming\Blender Foundation\Blender\2.75\scripts\addons
    * Mac: /Applications/Blender/blender.app/Contents/MacOS/2.75/scripts/addons

## Problems

* load.py:readBvhFile で ssFactor が 0 になり、0 剰余算例外が発生する問題
  * "frame % ssFactor == 0 and" で例外 (load.py:240)。
  * scn.McpDefaultSS が true になっていると .bvh ファイルのフレーム数から ssFactor が算出される (load.py:225)。
  * でも ssFactor の計算式は "int(1.0/(scn.render.fps * frameTime) + 0.49)"、これが 0 以上になるかどうかは frameTime の値による (load.py:223)。
  * おそらく .bvh に格納されている frameTime の値に秘密がある。

