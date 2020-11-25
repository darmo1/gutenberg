# gutenberg

/*
*    Enqueue Block Editor only Javascript and CSS
 */

function gb_menneskene_editor_scripts(){

    //Make paths variable so we don't write em  twice;
    $blockPath = '/assets/js/editor.blocks.js';
    $editorStylePath = '/assets/css/blocks.editor.css';

    //Enqueue the bundled block JS file
    wp_enqueue_script(
        'gb-menneskene-block-js', 
        plugins_url($blockPath, __FILE__ ), 
        ['wp-blocks', 'wp-i18n', 'wp-element','wp-editor','wp-components'], 
        filemtime( plugin_dir_path(__FILE__). $blockPath), 
    );

    //Enqueue optional editor Only Styles
    wp_enqueue_style(
        'gb-menneskene-block-style-editor', 
        plugins_url($editorStylePath, __FILE__ ), 
        ['wp-blocks'], 
        filemtime( plugin_dir_path(__FILE__).$editorStylePath), 
    );

}

//Hooks scripts function into block editor hook
add_action('enqueue_block_editor_assets', 'gb_menneskene_editor_scripts');

/*
*Enqueue front end and editor JavaScript and CSS
*/

function gb_menneskene_scripts(){
    $blockPath = '/assets/js/frontend.blocks.js';
    $stylePath = '/assets/css/blocks.style.css';

    if( !is_admin() ){
        //Enqueue the frontend JS file
        wp_enqueue_script(
            'gb-menneskene-block-frontend-js',
            plugins_url($blockPath, __FILE__ ), 
            ['wp-blocks', 'wp-i18n', 'wp-element','wp-editor','wp-components'], 
            filemtime( plugin_dir_path(__FILE__). $blockPath), 
        );
    }

    //Enqueue frontend and Editor block Styles
    wp_enqueue_style(
        'gb-menneskene-block-css',
        plugins_url($stylePath, __FILE__ ), 
        ['wp-blocks'], 
        filemtime( plugin_dir_path(__FILE__).$stylePath)
    );
}

//Hook scripts function into frontend and block editor
add_action('enqueue_block_assets', 'gb_menneskene_scripts');
