### uml: class diagram
```plantuml
@startuml
'autoactivate on
activate WasmExecutor
WasmExecutor -> WasmExecutor: call()
    activate WasmExecutor

    ' Call to Module
    'hnote over WasmExecutor: A Note
    WasmExecutor -> "wasmi::Module": from_buffer()
        activate "wasmi::Module"
        "wasmi::Module" --> WasmExecutor: TODO
        deactivate "wasmi::Module"


    ' START "instantiate_module" section
    WasmExecutor -> WasmExecutor: instantiate_module()
        activate WasmExecutor #005500
        create "wasmi::ModuleInstance"
        WasmExecutor -> "wasmi::ModuleInstance": new()
            activate "wasmi::ModuleInstance"
            "wasmi::ModuleInstance" --> WasmExecutor
            deactivate "wasmi::ModuleInstance"

        WasmExecutor -> WasmExecutor: get_heap_base()
            activate WasmExecutor
            WasmExecutor -> "wasmi::ModuleInstance":  not_started_instance()
                activate "wasmi::ModuleInstance"
                WasmExecutor <-- "wasmi::ModuleInstance": TODO
                deactivate "wasmi::ModuleInstance"
            deactivate WasmExecutor

        WasmExecutor -> WasmExecutor: gem_mem_instance()
            activate WasmExecutor
            WasmExecutor -> "wasmi::ModuleInstance": not_started_instance()
                activate "wasmi::ModuleInstance"
                WasmExecutor <-- "wasmi::ModuleInstance": TODO
                deactivate "wasmi::ModuleInstance"
            deactivate WasmExecutor

        WasmExecutor <-- WasmExecutor: TODO
        deactivate WasmExecutor
    ' END "instantiate_module" section

    WasmExecutor -> WasmExecutor: call_in_wasm_module()
        ' ...
        activate WasmExecutor
        WasmExecutor -> WasmExecutor: call_in_wasm_module_with_custom_signature()
        activate WasmExecutor

'... todo

@enduml
```

    class WasmExecutor {
        // Executes the provided code in a sandboxed wasm runtime
        ==
        + new()
        + call()
        + call_with_custom_signature()
        + get_mem_instance()
        + get_heap_base()
        + call_in_wasm_module()
        + call_in_wasm_module_with_custom_signature()
        + instantiate_module()
    }